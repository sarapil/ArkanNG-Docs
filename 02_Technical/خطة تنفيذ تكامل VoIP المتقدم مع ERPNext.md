

# **خطة تنفيذ تكامل VoIP المتقدم مع ERPNext**

## **مقدمة**

تهدف هذه الوثيقة إلى تقديم خارطة طريق معمارية وتقنية لتنفيذ تكامل عميق بين نظام ERPNext ومنصة اتصالات عبر بروتوكول الإنترنت (VoIP) مفتوحة المصدر. يتجاوز هذا التكامل مجرد ربط المكالمات؛ فهو يهدف إلى إنشاء نظام عصبي مركزي للاتصالات، مدعوم بالذكاء الاصطناعي، وقادر على أتمتة المهام التسويقية، وتحليل جودة التفاعل مع العملاء، وتوفير بنية تحتية مرنة وقابلة للتطوير.

---

## **القسم الأول: القرار المعماري \- اختيار منصة الـ PBX الأساسية**

### **1.1. بيان المشكلة والسياق**

الاختيار الأول والأكثر أهمية هو تحديد منصة PBX التي ستكون بمثابة العمود الفقري لنظام الاتصالات. يجب أن تكون هذه المنصة قابلة للتطوير، مرنة، ومفتوحة المصدر، مع واجهة برمجة تطبيقات (API) قوية تسمح بالتكامل العميق المطلوب لميزات مثل CTI (تكامل телефония الحاسوب)، AutoDialer، وتحليل المكالمات.

### **1.2. الخيارات المدروسة**

1. **الخيار أ: FreePBX \+ Asterisk:** الحل الأكثر شيوعًا وانتشارًا في عالم VoIP مفتوح المصدر. Asterisk هو المحرك الأساسي، و FreePBX هو واجهة المستخدم الرسومية (GUI) التي تسهل إدارته.  
2. **الخيار ب: FusionPBX \+ FreeSwitch:** حل أحدث مصمم لمعالجة بعض القيود المعمارية في Asterisk. FreeSwitch هو المحرك، و FusionPBX هو واجهة المستخدم الرسومية متعددة المستأجرين (Multi-Tenant).

### **1.3. تحليل ومقارنة**

| المعيار | FreePBX \+ Asterisk | FusionPBX \+ FreeSwitch | التحليل |
| ----: | ----: | ----: | ----: |
| **المعماریة** | متجانسة (Monolithic). تعمل جميع الميزات كجزء من نواة واحدة.1 | معيارية (Modular). يمكن تحميل المكونات أو إزالتها حسب الحاجة، مما يقلل من استهلاك الموارد.1 | معمارية FreeSwitch المعيارية أكثر ملاءمة للتطبيقات المعقدة والقابلة للتطوير. |
| **قابلية التوسع** | جيدة ولكنها تتطلب ضبطًا دقيقًا للتعامل مع الأحمال العالية. قد تواجه تحديات في ظل عدد كبير من المكالمات المتزامنة.2 | ممتازة. مصممة للتعامل مع آلاف المكالمات المتزامنة بكفاءة، مما يجعلها مثالية للبيئات الكبيرة ومراكز الاتصال.3 | يتفوق FreeSwitch بشكل واضح في قابلية التوسع، وهو أمر حاسم لنظام AutoDialer. |
| **دعم Multi-Tenant** | غير مدعوم أصلاً. يتطلب حلولاً معقدة وغير رسمية.5 | ميزة أساسية ومدمجة. FusionPBX مصمم من الألف إلى الياء ليكون نظامًا متعدد المستأجرين، مما يسهل تقديم الخدمة لعملاء متعددين.5 | FusionPBX هو الخيار الأفضل إذا كان هناك أي تخطيط مستقبلي لتقديم خدمات PBX لعملاء خارجيين. |
| **واجهة برمجة التطبيقات (API)** | **AMI (Asterisk Manager Interface):** واجهة قوية ولكنها أقدم. يمكن أن تكون معقدة للتعامل مع الأحداث في الوقت الفعلي.7 | **ESL (Event Socket Library):** تعتبر أكثر حداثة ومرونة وقوة، ومصممة للتفاعل العميق مع منطق المكالمات.4 | ESL في FreeSwitch توفر تحكمًا أدق وأكثر قوة، وهو أمر ضروري لتنفيذ CTI وتحليل المكالمات المتقدم. |
| **الميزات المدمجة** | يتطلب وحدات تجارية مدفوعة للعديد من الميزات المتقدمة مثل Call Center.6 | يقدم FusionPBX ميزات متقدمة مثل Call Center وإدارة قوائم الانتظار بشكل مجاني ومفتوح المصدر.6 | يقدم FusionPBX قيمة أكبر "خارج الصندوق" مع ميزات أساسية لأهداف المشروع. |
| **الاستقرار والدعم** | مجتمع ضخم ولكن التحديثات قد تسبب مشاكل عدم استقرار.5 | مجتمع أصغر ولكنه أكثر تركيزًا على المطورين. يُعرف FreeSwitch باستقراره تحت الأحمال العالية.4 | الاستقرار الذي يوفره FreeSwitch يجعله خيارًا أكثر أمانًا لبيئة الإنتاج. |

### **1.4. القرار النهائي**

**الخيار المختار: FusionPBX \+ FreeSwitch.**

**التبرير:** على الرغم من أن Asterisk يتمتع بمجتمع أكبر، إلا أن التفوق المعماري لـ FreeSwitch في قابلية التوسع، والاستقرار، وقوة واجهة ESL API يجعله الخيار الأنسب للأهداف طويلة المدى لهذا المشروع. إن دعم FusionPBX الأصلي لـ Multi-Tenancy وميزات مركز الاتصال المجانية يوفر أساسًا أقوى وأكثر فعالية من حيث التكلفة لبناء نظام الاتصالات المتكامل المطلوب.

---

## **القسم الثاني: القرار المعماري \- اختيار Web SIP Client**

### **2.1. بيان المشكلة والسياق**

لتوفير تجربة مستخدم سلسة، يجب تضمين هاتف برمجي (Softphone) يعمل بتقنية WebRTC مباشرة داخل واجهة مستخدم ERPNext. هذا يتطلب اختيار مكتبة JavaScript SIP قوية وموثوقة.

### **2.2. الخيارات المدروسة**

1. **الخيار أ: SIPml5:** واحدة من أقدم مكتبات HTML5 SIP وأكثرها شمولاً من حيث الميزات.11  
2. **الخيار ب: JsSIP:** مكتبة JavaScript خفيفة الوزن وحديثة تركز على البساطة والامتثال للمعايير.13

### **2.3. تحليل ومقارنة**

| المعيار | SIPml5 | JsSIP | التحليل |
| ----: | ----: | ----: | ----: |
| **الموثوقية والجودة** | قوية ولكنها قد تتطلب "RTCWeb Breaker" للتوافق مع بعض الخوادم مثل FreeSwitch، مما يضيف طبقة من التعقيد.15 | تعتبر الأكثر موثوقية وجودة في الشيفرة البرمجية بين الخيارات المتاحة.16 | موثوقية JsSIP تجعلها خيارًا أكثر أمانًا لتقليل مشاكل التصحيح على المدى الطويل. |
| **الخفة والبساطة** | مكتبة كبيرة نسبيًا (\~1 Mo) مع مجموعة واسعة من الميزات.11 | خفيفة الوزن ومصممة لتكون بسيطة وسهلة الاستخدام مع واجهة API قوية.13 | بساطة JsSIP تجعل عملية التكامل مع واجهة ERPNext أسرع وأسهل. |
| **التوافق مع الخوادم** | تدعم Asterisk و FreeSwitch (مع RTCWeb Breaker).15 | تعمل بشكل ممتاز مع Asterisk و Kamailio و OverSIP وغيرها من الخوادم المتوافقة مع SIP over WebSocket.14 | كلتا المكتبتين متوافقتان، لكن JsSIP قد تتطلب خطوات أقل لتحقيق التكامل. |
| **المجتمع والتوثيق** | التوثيق متاح ولكن المشروع يبدو أقل نشاطًا في السنوات الأخيرة.12 | مجتمع نشط، توثيق واضح، ومكتوبة من قبل مؤلفي RFC 7118، مما يضمن الامتثال للمعايير.14 | التوثيق الحديث والمجتمع النشط لـ JsSIP يمثلان ميزة كبيرة للتطوير والصيانة. |

### **2.4. القرار النهائي**

**الخيار المختار: JsSIP.**

**التبرير:** JsSIP هي الخيار الأفضل نظرًا لكونها مكتبة حديثة، خفيفة الوزن، وموثوقة. واجهتها البرمجية النظيفة والتوثيق الممتاز والتركيز على الامتثال للمعايير سيجعل عملية دمج هاتف WebRTC في واجهة ERPNext أكثر سلاسة واستقرارًا.

---

## **القسم الثالث: خطة التنفيذ التفصيلية**

سيتم تنفيذ المشروع على مراحل، بناءً على القرارات المعمارية السابقة.

### **3.1. المرحلة الأولى: بناء وحدة CTI الأساسية**

**الهدف:** ربط ERPNext بـ FreeSwitch لتمكين الميزات الأساسية لتكامل الاتصالات.

**المكونات:**

1. **تطبيق Frappe مخصص (VoIP\_Integration):**  
   * **DocTypes جديدة:**  
     * SIP Extension: لتخزين تفاصيل الامتدادات (الرقم، كلمة المرور) وربطها بـ User DocType في ERPNext.  
     * Call Log: لتسجيل جميع المكالمات الواردة والصادرة (المتصل، المستقبل، المدة، حالة المكالمة، رابط التسجيل).  
   * **تضمين JsSIP في واجهة Desk UI:**  
     * سيتم إضافة هاتف WebRTC كعنصر ثابت في واجهة المستخدم (على سبيل المثال، في الشريط الجانبي أو السفلي).  
     * عند تسجيل دخول المستخدم إلى ERPNext، سيقوم الـ Client Script بتسجيل امتداده تلقائيًا في FreeSwitch.  
   * **خدمة CTI Listener (وسيط):**  
     * سيتم تطوير خدمة Python مستقلة (يمكن تشغيلها كـ background worker) تتصل بـ FreeSwitch عبر **Event Socket Library (ESL)** باستخدام مكتبة مثل python-esl.19  
     * ستستمع هذه الخدمة للأحداث الهامة في الوقت الفعلي (مثل CHANNEL\_CREATE, CHANNEL\_ANSWER, CHANNEL\_HANGUP).  
     * عند وقوع حدث، ستقوم الخدمة بمعالجته وإرسال البيانات إلى ERPNext عبر واجهة برمجة التطبيقات REST لإنشاء أو تحديث سجلات Call Log.  
   * **تنفيذ ميزات CTI:**  
     * **Screen Pop:** عندما تستقبل خدمة CTI Listener حدث مكالمة واردة، ستقوم بالبحث عن رقم المتصل في Customer أو Lead DocTypes. إذا تم العثور عليه، سترسل إشعارًا في الوقت الفعلي إلى واجهة المستخدم (عبر Frappe Socket.IO) لفتح صفحة العميل تلقائيًا.  
     * **Click-to-Call:** سيتم إضافة زر "اتصال" بجانب حقول الهاتف في ERPNext. عند النقر عليه، سيقوم Client Script باستدعاء Server Script من نوع 'API' عبر frappe.call.20 سيقوم الـ Server Script بإرسال أمر إلى خدمة CTI Listener لبدء مكالمة عبر إجراء  
       Originate في FreeSwitch.  
     * **Automatic Call Logging:** سيتم تسجيل جميع المكالمات تلقائيًا في Call Log DocType بواسطة خدمة CTI Listener، مع ربطها بالعميل أو المستخدم المعني.

### **3.2. المرحلة الثانية: تطوير نظام AutoDialer الذكي**

**الهدف:** أتمتة حملات الاتصال الصادرة وتحليل نتائجها باستخدام الذكاء الاصطناعي.

**المكونات:**

1. **وحدة إدارة الحملات في ERPNext:**  
   * **DocTypes جديدة:**  
     * Dialer Campaign: لتحديد الحملة، الفئة المستهدفة (من Lead أو Customer Group)، الجدول الزمني، وسيناريو المكالمة.  
     * Call Script: لتخزين نصوص المكالمات المختلفة.  
   * **منطق المتصل التلقائي (AutoDialer Logic):**  
     * سيتم إنشاء Scheduled Server Script يعمل كل دقيقة.  
     * سيقوم السكريبت بالبحث عن الحملات النشطة، واختيار العميل التالي للاتصال به بناءً على القواعد (مثل عدم الاتصال مرة أخرى في نفس اليوم).  
     * سيقوم بإرسال أمر إلى خدمة CTI Listener لبدء المكالمة.  
2. **تكامل الذكاء الاصطناعي لتحليل المكالمات (FastAPI Microservice):**  
   * سيتم استخدام نفس الخدمة المصغرة FastAPI التي تم تصميمها مسبقًا.  
   * **سير العمل:**  
     1. بعد انتهاء المكالمة، يقوم FreeSwitch بحفظ التسجيل الصوتي.  
     2. تكتشف خدمة CTI Listener انتهاء المكالمة وتحصل على مسار ملف التسجيل.  
     3. ترسل خدمة CTI Listener طلبًا إلى FastAPI microservice مع مسار التسجيل ومعرف سجل المكالمة في ERPNext.  
     4. تقوم خدمة FastAPI بتفريغ المكالمة باستخدام **Whisper** (للدقة العالية) و **Qwen-Voice** (لتحسين الأداء باللغة العربية).22  
     5. تقوم بتحليل النص لتحديد المشاعر والكلمات المفتاحية.  
     6. ترسل النتائج (النص، تحليل المشاعر) مرة أخرى إلى ERPNext عبر واجهة برمجة التطبيقات لتحديث سجل Call Log المقابل.  
3. **إدارة النتائج في ERPNext:**  
   * سيتم تحديث Call Log تلقائيًا بحالة المكالمة (ناجحة، غير مهتم، متابعة).  
   * بناءً على تحليل الذكاء الاصطناعي، يمكن إنشاء مهام متابعة (ToDo) تلقائيًا للمسوقين.

### **3.3. المرحلة الثالثة: بناء لوحة تحكم متقدمة لتحليل المكالمات**

**الهدف:** تزويد المشرفين بأدوات قوية لتقييم أداء المسوقين وتحسين الاستراتيجيات.

**المكونات:**

1. **لوحة تحكم للمشرف (Supervisor Dashboard) في ERPNext:**  
   * سيتم إنشاء صفحة مخصصة تعرض تقارير مفصلة عن المكالمات.  
   * **الميزات:**  
     * عرض نص المكالمة الكامل مع تحديد المتحدث.  
     * رسم بياني زمني لتحليل المشاعر (للمسوق والعميل).  
     * تقرير أداء تلقائي يقيم مدى الالتزام بالسكريبت، الاستماع الفعال، إلخ.  
     * نصائح تحسين مولدة بواسطة الذكاء الاصطناعي.  
     * إمكانية إضافة ملاحظات يدوية من قبل المشرف.  
2. **محرك تقييم الأداء (في FastAPI Microservice):**  
   * سيتم توسيع الخدمة المصغرة لتشمل منطق تقييم الأداء.  
   * باستخدام نموذج لغوي كبير (LLM) وموجهات متقدمة، سيقوم النظام بمقارنة نص المكالمة مع Call Script المخزن في ERPNext وتقييم أداء المسوق بناءً على المعايير المحددة.

### **3.4. المرحلة الرابعة: ضمان استمرارية الخدمة (High Availability)**

**الهدف:** توفير آلية اتصال احتياطية لضمان استمرارية العمل عند انقطاع الإنترنت.

**المكونات:**

1. **التكامل مع GSM Gateway:**  
   * **الأجهزة:** سيتم استخدام بوابة GSM متوافقة مع Asterisk/FreeSwitch، مثل تلك التي تدعم وحدات **Quectel EC25 Series**.26  
   * **التكوين في FreeSwitch:**  
     * سيتم تكوين بوابة GSM كـ "Trunk" إضافي في FreeSwitch.  
     * سيتم تعديل خطة الاتصال الصادرة (Outbound Dialplan) لتشمل منطق تجاوز الفشل (Failover).  
     * **المنطق:** حاول الاتصال عبر Trunk\_SIP\_الأساسي. إذا فشل، حاول الاتصال عبر Trunk\_GSM\_الاحتياطي.  
   * **النتيجة:** سيتحول النظام تلقائيًا لاستخدام شبكة الموبايل لإجراء المكالمات الصادرة في حالة انقطاع اتصال الإنترنت الأساسي، مما يقلل من انقطاع المكالمات بشكل كبير.

---

## **القسم الرابع: واجهة المستخدم ومؤشرات الأداء الرئيسية (KPIs)**

### **4.1. تصميم واجهة المستخدم (مقترح)**

* **لوحة التحكم الرئيسية:** ستعرض ملخصًا حيًا للحملات النشطة، إجمالي المكالمات، معدلات الإجابة والتحويل، وأداء أفضل المسوقين.  
* **صفحة تفاصيل الحملة:** ستعرض جميع المعلومات المتعلقة بحملة معينة، بما في ذلك قائمة العملاء، وحالة كل مكالمة، وتحليل النتائج المجمعة للحملة.  
* **صفحة تحليل المكالمة:** ستكون جزءًا من Call Log DocType، وتعرض النص الكامل، التحليل الزمني للمشاعر، تقرير الأداء، والملاحظات.

### **4.2. مؤشرات الأداء الرئيسية (KPIs)**

سيتم تتبع المؤشرات التالية لضمان نجاح النظام:

| الفئة | المؤشر (KPI) | الهدف | الأداة |
| ----- | ----: | ----: | ----: |
| **أداء النظام** | وقت التشغيل (Uptime) | \> 99.9% | أدوات مراقبة مثل Zabbix |
|  | وقت استجابة النظام | \< 500 مللي ثانية | أدوات مراقبة مثل SmokePing |
| **أداء AutoDialer** | عدد المكالمات اليومية | 500+ | تقارير ERPNext المخصصة |
|  | معدل الإجابة | \> 35% | تقارير ERPNext المخصصة |
|  | معدل التحويل (Conversion Rate) | \> 15% | تقارير ERPNext المخصصة |
| **أداء الفرق** | تحسن إنتاجية الفريق | \> 150% | مقارنة الأداء قبل وبعد التنفيذ |
|  | تحسن أداء المسوقين (متوسط الدرجات) | زيادة بنسبة 35% | لوحة تحكم المشرف |
|  | تقليل شكاوى العملاء | \> 25% | سجلات الدعم الفني |

#### **Works cited**

1. FreeSWITCH Vs. Asterisk— What Fits Your Business Best in 2025?, accessed September 12, 2025, [https://www.asteriskservice.com/blog/freeswitch-vs-asterisk-what-fits-your-business-best/](https://www.asteriskservice.com/blog/freeswitch-vs-asterisk-what-fits-your-business-best/)  
2. Asterisk vs FreeSWITCH \- Which One To Choose For Business? \- Ecosmob, accessed September 12, 2025, [https://www.ecosmob.com/asterisk-vs-freeswitch/](https://www.ecosmob.com/asterisk-vs-freeswitch/)  
3. Asterisk vs FreeSWITCH – Which One is Best for Your VoIP Solutions?, accessed September 12, 2025, [https://sheerbit.com/asterisk-vs-freeswitch-which-one-is-best-for-your-voip-solutions/](https://sheerbit.com/asterisk-vs-freeswitch-which-one-is-best-for-your-voip-solutions/)  
4. FreeSWITCH vs Asterisk: Which VoIP Platform Is Right for You? \- DEV Community, accessed September 12, 2025, [https://dev.to/sheerbittech/freeswitch-vs-asterisk-which-voip-platform-is-right-for-you-5gcn](https://dev.to/sheerbittech/freeswitch-vs-asterisk-which-voip-platform-is-right-for-you-5gcn)  
5. FusionPBX vs. FreePBX : r/VOIP \- Reddit, accessed September 12, 2025, [https://www.reddit.com/r/VOIP/comments/78wyt7/fusionpbx\_vs\_freepbx/](https://www.reddit.com/r/VOIP/comments/78wyt7/fusionpbx_vs_freepbx/)  
6. NEW \- The Taming of FusionPBX \+ Tutorial | The VoIP-info Forum, accessed September 12, 2025, [https://www.voip-info.org/forum/threads/the-taming-of-fusionpbx-tutorial.28210/](https://www.voip-info.org/forum/threads/the-taming-of-fusionpbx-tutorial.28210/)  
7. Yah, I think this is the right answer. FreeSwitch is a great deal newer than ast... | Hacker News, accessed September 12, 2025, [https://news.ycombinator.com/item?id=21420840](https://news.ycombinator.com/item?id=21420840)  
8. Python with FreeSWITCH & Asterisk: VoIP Dev in 2025 \- Magic Technolabs, accessed September 12, 2025, [https://www.magictechnolabs.com/blog/python-with-freeswitch-asterisk-voip-dev-in-2025/](https://www.magictechnolabs.com/blog/python-with-freeswitch-asterisk-voip-dev-in-2025/)  
9. FreeSWITCh \- Nick vs Networking, accessed September 12, 2025, [https://nickvsnetworking.com/tag/freeswitch/](https://nickvsnetworking.com/tag/freeswitch/)  
10. FreePBX vs. FusionPBX Comparison \- SourceForge, accessed September 12, 2025, [https://sourceforge.net/software/compare/FreePBX-vs-FusionPBX/](https://sourceforge.net/software/compare/FreePBX-vs-FusionPBX/)  
11. sipML5 \- The world's first open source HTML5 SIP client, accessed September 12, 2025, [https://scripts.netformatie.nl/n4mrtc/](https://scripts.netformatie.nl/n4mrtc/)  
12. sipML5 \- Google Code, accessed September 12, 2025, [https://code.google.com/archive/p/sipml5/](https://code.google.com/archive/p/sipml5/)  
13. rtckit/awesome-rtc: :satellite: A curated list of awesome Real Time Communications resources \- GitHub, accessed September 12, 2025, [https://github.com/rtckit/awesome-rtc](https://github.com/rtckit/awesome-rtc)  
14. Overview \- JsSIP, accessed September 12, 2025, [https://jssip.net/documentation/overview/](https://jssip.net/documentation/overview/)  
15. sipml5 \- FAQ.wiki \- Google Code, accessed September 12, 2025, [https://code.google.com/archive/p/sipml5/wikis/FAQ.wiki](https://code.google.com/archive/p/sipml5/wikis/FAQ.wiki)  
16. (PDF) Comparative analysis of SIP-libraries. Improvements of JsSIP library \- ResearchGate, accessed September 12, 2025, [https://www.researchgate.net/publication/324778752\_Comparative\_analysis\_of\_SIP-libraries\_Improvements\_of\_JsSIP\_library](https://www.researchgate.net/publication/324778752_Comparative_analysis_of_SIP-libraries_Improvements_of_JsSIP_library)  
17. Interoperability \- JsSIP, accessed September 12, 2025, [https://jssip.net/documentation/misc/interoperability/](https://jssip.net/documentation/misc/interoperability/)  
18. JsSIP \- the Javascript SIP library, accessed September 12, 2025, [https://jssip.net/](https://jssip.net/)  
19. Event Socket Library | FreeSWITCH Documentation, accessed September 12, 2025, [https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Client-and-Developer-Interfaces/Event-Socket-Library/](https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Client-and-Developer-Interfaces/Event-Socket-Library/)  
20. Python ESL | FreeSWITCH Documentation, accessed September 12, 2025, [https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Client-and-Developer-Interfaces/Python-ESL/](https://developer.signalwire.com/freeswitch/FreeSWITCH-Explained/Client-and-Developer-Interfaces/Python-ESL/)  
21. Mizutech Wiki \> Compare Web SIP client solutions \- Mizu VoIP, accessed September 12, 2025, [https://www.mizu-voip.com/Support/Wiki/tabid/99/Default.aspx?topic=Compare+Web+SIP+client+solutions](https://www.mizu-voip.com/Support/Wiki/tabid/99/Default.aspx?topic=Compare+Web+SIP+client+solutions)  
22. Live Speech To Text in Arabic : r/LocalLLaMA \- Reddit, accessed September 12, 2025, [https://www.reddit.com/r/LocalLLaMA/comments/1lc4j2w/live\_speech\_to\_text\_in\_arabic/](https://www.reddit.com/r/LocalLLaMA/comments/1lc4j2w/live_speech_to_text_in_arabic/)  
23. Qwen Audio: Text Generation from Audio Input | by David Cochard | ailia-ai | Medium, accessed September 12, 2025, [https://medium.com/axinc-ai/qwen-audio-text-generation-from-audio-input-c77a8afb25d4](https://medium.com/axinc-ai/qwen-audio-text-generation-from-audio-input-c77a8afb25d4)  
24. Huzaifa7524/Whisper\_small\_openai\_finetuned\_on\_arabic\_language: Arabic Speech Recognition with Whisper \- GitHub, accessed September 12, 2025, [https://github.com/Huzaifa7524/Whisper\_small\_openai\_finetuned\_on\_arabic\_language](https://github.com/Huzaifa7524/Whisper_small_openai_finetuned_on_arabic_language)  
25. Speech-to-text Models | CCV AI Services, accessed September 12, 2025, [https://docs.ccv.brown.edu/ai-tools/services/transcribe/speech-to-text-models](https://docs.ccv.brown.edu/ai-tools/services/transcribe/speech-to-text-models)  
26. ca4ti/asterisk-chan-quectel \- GitHub, accessed September 12, 2025, [https://github.com/ca4ti/asterisk-chan-quectel](https://github.com/ca4ti/asterisk-chan-quectel)  
27. chan\_quectel channel driver for Quectel LTE cards, works with Asterisk-13+ \- GitHub Pages, accessed September 12, 2025, [https://t4rd15.github.io/asterisk-chan-quectel/](https://t4rd15.github.io/asterisk-chan-quectel/)  
28. Asterisk chan\_dongle with Quectel and Simcom modules | The VoIP-info Forum, accessed September 12, 2025, [https://www.voip-info.org/forum/threads/asterisk-chan\_dongle-with-quectel-and-simcom-modules.26022/](https://www.voip-info.org/forum/threads/asterisk-chan_dongle-with-quectel-and-simcom-modules.26022/)