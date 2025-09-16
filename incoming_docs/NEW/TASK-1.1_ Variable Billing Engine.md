

## **المواصفات الفنية: محرك الفوترة المتغيرة (القائمة على الاستخدام)**

المهمة ID: TASK-1.1  
المرحلة: 1 \- بناء الأساس التشغيلي والتجاري  
الوثائق ذات الصلة: Business\_Model\_and\_Pricing\_Strategy (v1.2), Integrated\_Ecosystem\_Architecture (v1.2)

### **1\. الهدف**

أتمتة عملية الفوترة الشهرية للعملاء في خدمة "مساحات العمل كخدمة"، بناءً على عدد الموظفين النشطين والخدمات الإضافية. هذا المحرك هو حجر الزاوية في نموذج الإيرادات المتكررة لدينا.

### **2\. التحليل التقني والتصميم**

تفتقر منصة Frappe/ERPNext إلى آلية مدمجة للفوترة المتغيرة القائمة على الاستخدام؛ فوحدة Subscription مصممة للمبالغ الثابتة المتكررة.\[1, 2\] لذلك، سنقوم ببناء حل مخصص باستخدام Server Script مجدول.

#### **2.1. نموذج البيانات (DocTypes)**

لا حاجة لـ DocTypes جديدة في هذه المرحلة. سنعتمد على DocTypes الحالية:

* **Company**: لتمثيل كل شركة عميلة.  
* **Employee (من Frappe HR)**: لتحديد الموظفين النشطين لكل شركة.  
* **Sales Invoice (من Frappe Books)**: المستند النهائي الذي سيتم إنشاؤه.  
* **Contract**: لتخزين الشروط التجارية الخاصة بكل عميل (مثل سعر المكتب لكل موظف). سنضيف حقلًا مخصصًا:  
  * **Monthly Rate Per Employee (Currency)**: لتخزين السعر الشهري المتفق عليه لكل موظف/مكتب.

#### **2.2. المنطق البرمجي (Server Script)**

سيتم إنشاء Server Script جديد بالخصائص التالية:

* **Script Type:** Scheduler Event  
* **Scheduler Event:** monthly (أو cron لتحديد يوم معين، مثل 0 0 25 \* \* للتشغيل في اليوم 25 من كل شهر).  
* **Script (Python):**

Python

import frappe  
from frappe.utils import nowdate, add\_months, get\_first\_day, get\_last\_day

def generate\_monthly\_usage\_invoices():  
    \# الحصول على تاريخ اليوم لتحديد الشهر المالي الحالي  
    today \= nowdate()  
    month\_start \= get\_first\_day(today)  
    month\_end \= get\_last\_day(today)

    \# الحصول على قائمة بجميع شركات العملاء النشطة (باستثناء شركتنا)  
    client\_companies \= frappe.get\_all("Company", filters={"is\_group": 0, "company\_name": \["\!=", "Arkan Labs"\]})

    for company\_data in client\_companies:  
        company\_name \= company\_data.name  
          
        \# البحث عن العقد النشط لهذا العميل  
        contract \= frappe.get\_doc("Contract", {"customer": company\_name, "status": "Active"})  
        if not contract or not contract.custom\_monthly\_rate\_per\_employee:  
            frappe.log\_error(f"No active contract or monthly rate for {company\_name}", "Billing Engine")  
            continue

        \# حساب عدد الموظفين النشطين في الشركة خلال هذا الشهر  
        active\_employees\_count \= frappe.db.count("Employee", {  
            "company": company\_name,  
            "status": "Active"  
        })

        if active\_employees\_count \== 0:  
            continue \# لا توجد فاتورة إذا لم يكن هناك موظفون

        \# حساب المبلغ الإجمالي للفاتورة  
        rate\_per\_employee \= contract.custom\_monthly\_rate\_per\_employee  
        total\_amount \= active\_employees\_count \* rate\_per\_employee

        \# إنشاء فاتورة مبيعات جديدة  
        try:  
            new\_invoice \= frappe.new\_doc("Sales Invoice")  
            new\_invoice.customer \= company\_name  
            new\_invoice.posting\_date \= month\_end  
            new\_invoice.due\_date \= add\_months(month\_end, 1) \# تاريخ الاستحقاق بعد شهر واحد  
            new\_invoice.company \= "Arkan Labs" \# الفاتورة تصدر من شركتنا

            \# إضافة بند الفاتورة  
            new\_invoice.append("items", {  
                "item\_code": "WORKSPACE-SERVICE", \# يجب إنشاء هذا الصنف كصنف خدمة  
                "item\_name": f"Workspace Service for {active\_employees\_count} employees for {frappe.utils.formatdate(month\_start, 'MMMM yyyy')}",  
                "qty": active\_employees\_count,  
                "rate": rate\_per\_employee,  
                "amount": total\_amount  
            })

            new\_invoice.insert(ignore\_permissions=True) \# تجاهل الأذونات لأن السكربت يعمل كمستخدم نظام  
            frappe.db.commit()  
            frappe.log\_error(f"Successfully created draft invoice {new\_invoice.name} for {company\_name}", "Billing Engine")

        except Exception as e:  
            frappe.log\_error(frappe.get\_traceback(), f"Invoice Creation Failed for {company\_name}")  
            frappe.db.rollback()

### **3\. التقنيات والمكتبات الرئيسية**

* **Frappe Framework:** Server Script, Scheduler, frappe.db.count, frappe.new\_doc, doc.insert(), frappe.log\_error.  
* **Python:** مكتبات frappe.utils للتعامل مع التواريخ.

### **4\. معايير القبول**

* عند تشغيل السكربت المجدول، يجب إنشاء فاتورة مبيعات (Sales Invoice) في حالة "مسودة" (Draft) لكل شركة عميلة لديها موظفون نشطون.  
* يجب أن يكون مبلغ الفاتورة مطابقًا لـ (عدد الموظفين النشطين \* السعر الشهري المحدد في عقد العميل).  
* يجب تسجيل أي أخطاء تحدث أثناء إنشاء الفواتير في Error Log الخاص بـ Frappe.  
* لا يتم إنشاء فواتير للشركات التي ليس لديها موظفون نشطون.

### **5\. المخاطر المحتملة والتخفيف منها**

* **الخطر:** أداء الاستعلام قد يتباطأ مع زيادة عدد الموظفين والشركات.  
  * **التخفيف:** الاستعلامات المستخدمة (frappe.db.count) بسيطة ومفهرسة جيدًا. يجب مراقبة أداء السكربت مع نمو البيانات.  
* **الخطر:** تغييرات في أسماء DocTypes أو الحقول في تحديثات Frappe المستقبلية قد تكسر السكربت.  
  * **التخفيف:** يجب أن يكون السكربت جزءًا من مجموعة الاختبارات الآلية لدينا لضمان اكتشاف أي مشاكل توافق مبكرًا.