

## **المواصفات الفنية: تكامل CTI الأساسي**

المهمة ID: TASK-1.2  
المرحلة: 1 \- بناء الأساس التشغيلي والتجاري  
الوثائق ذات الصلة: Integrated\_Ecosystem\_Architecture (v1.2), Omnichannel\_Communication\_Strategy (v1.2)

### **1\. الهدف**

دمج نظام الاتصالات FreeSwitch مع منصة **ArkanNG** لتوفير ميزات تكامل الاتصالات الهاتفية الحاسوبية (CTI) الأساسية: **Screen Pop** (عرض ملف العميل تلقائيًا عند ورود مكالمة) و **Click-to-Call** (بدء المكالمات بنقرة واحدة من داخل المنصة).

### **2\. التحليل التقني والتصميم**

هذا التكامل يتطلب ثلاثة مكونات رئيسية تعمل معًا: خدمة خلفية تستمع لأحداث FreeSwitch، واجهة برمجة تطبيقات في ArkanNG لتلقي الأوامر، وسكربتات من جانب العميل في واجهة المستخدم.

#### **2.1. خدمة CTI Listener (الوسيط)**

هذه ستكون خدمة Python مستقلة تعمل بشكل مستمر.

* **البنية:** خدمة asyncio تستخدم مكتبة python-esl للاتصال بـ FreeSwitch Event Socket Library (ESL) في وضع "Inbound".\[3, 4\]  
* **الاتصال:** ستتصل الخدمة بـ FreeSwitch ESL على المنفذ المحدد (عادة 8021\) وتصادق باستخدام كلمة المرور المحددة في event\_socket.conf.xml.  
* **المنطق:**  
  1. عند الاتصال، تشترك في الأحداث الهامة: CHANNEL\_CREATE, CHANNEL\_ANSWER, CHANNEL\_HANGUP, CHANNEL\_BRIDGE.\[5, 6\]  
  2. **لميزة Screen Pop:** عند استقبال حدث CHANNEL\_CREATE لمكالمة واردة، ستقوم الخدمة بما يلي:  
     * استخراج رقم المتصل (Caller-Caller-ID-Number).  
     * إجراء استدعاء API إلى ArkanNG (عبر requests) للبحث عن هذا الرقم في Lead و Customer DocTypes.  
     * إذا تم العثور على تطابق، تقوم بإرسال حدث عبر **WebSocket (Socket.IO)** إلى واجهة مستخدم ArkanNG، يحتوي على doctype و docname الخاص بالعميل.  
  3. **لميزة Click-to-Call:** ستعرض الخدمة نقطة نهاية (endpoint) بسيطة (باستخدام FastAPI أو Flask) لتلقي طلبات بدء المكالمات من ArkanNG. عند تلقي طلب، ستقوم بإرسال أمر originate إلى FreeSwitch عبر ESL.\[7, 8\]

#### **2.2. واجهة برمجة التطبيقات وسكربتات الخادم في ArkanNG**

* **Server Script (API):** سيتم إنشاء Server Script من نوع 'API' يسمى initiate\_call.  
  * **الوظيفة:** سيتلقى هذا السكربت رقم الهاتف واسم المستخدم من Client Script.  
  * سيقوم بإجراء استدعاء frappe.make\_post\_request إلى نقطة نهاية "originate" في خدمة CTI Listener.\[9, 10\]  
  * هذا يوفر طبقة أمان، حيث أن الواجهة الأمامية لا تتصل بخدمة CTI مباشرة.

#### **2.3. سكربتات العميل (Client Scripts)**

* **لـ Click-to-Call:**  
  * سيتم إنشاء Client Script يتم تطبيقه على نماذج Lead و Customer.  
  * سيستخدم frm.add\_custom\_button لإضافة زر "اتصال" بجانب حقول الهاتف.\[11, 12\]  
  * عند النقر على الزر، سيتم تشغيل frappe.call لاستدعاء Server Script initiate\_call، مع تمرير رقم الهاتف.\[13\]  
* **لـ Screen Pop:**  
  * سيتم تعديل سكربت JavaScript العام لواجهة Desk.  
  * سيستخدم frappe.realtime.on للاستماع إلى حدث WebSocket المخصص (مثل show\_customer\_popup).\[14\]  
  * عند استقبال الحدث، سيستخدم frappe.set\_route لفتح صفحة العميل المستلمة في الحدث (/app/\[doctype\]/\[docname\]).

### **3\. التقنيات والمكتبات الرئيسية**

* **FreeSwitch:** Event Socket Library (ESL).  
* **Python (لخدمة CTI Listener):** python-esl, asyncio, requests, fastapi.  
* **Frappe Framework:** Server Script (API), Client Script, frappe.call, frappe.make\_post\_request, frappe.realtime.on, frappe.set\_route.

### **4\. معايير القبول**

* عند ورود مكالمة من رقم موجود في النظام، يجب أن تفتح صفحة العميل أو العميل المحتمل المقابلة تلقائيًا في واجهة المستخدم.  
* يجب أن يظهر زر "اتصال" بجانب حقول الهاتف في نماذج Lead و Customer.  
* عند النقر على زر "اتصال"، يجب أن تبدأ مكالمة صادرة إلى الرقم المحدد.

### **5\. المخاطر المحتملة والتخفيف منها**

* **الخطر:** انقطاع الاتصال بين خدمة CTI Listener و FreeSwitch.  
  * **التخفيف:** يجب أن تتضمن خدمة CTI Listener منطقًا قويًا لإعادة الاتصال التلقائي مع تراجع أسي (exponential backoff).  
* **الخطر:** تأخير في Screen Pop بسبب بطء البحث في قاعدة البيانات.  
  * **التخفيف:** يجب التأكد من أن حقول أرقام الهواتف في Lead و Customer مفهرسة بشكل صحيح في قاعدة البيانات.