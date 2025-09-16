

## **المواصفات الفنية: تطبيق إدارة مساحات العمل**

المهمة ID: TASK-1.3  
المرحلة: 1 \- بناء الأساس التشغيلي والتجاري  
الوثائق ذات الصلة: Arkan\_Labs\_Workspace\_Management\_System (v1.0)

### **1\. الهدف**

إنشاء "توأم رقمي" لمساحة العمل المادية داخل منصة **ArkanNG**، مما يتيح إدارة وتتبع وحجز الموارد المادية (المكاتب، غرف الاجتماعات) بشكل مركزي ومنظم.

### **2\. التحليل التقني والتصميم**

سيتم بناء هذا الحل كتطبيق Frappe مخصص جديد يسمى workspace\_management.

#### **2.1. نموذج البيانات (DocTypes)**

سيتم إنشاء مجموعة من DocTypes المخصصة والمترابطة لنمذجة البيئة المادية بشكل هرمي.\[15, 16\]

1. **Building (مبنى):**  
   * building\_name (Data, Mandatory)  
   * address (Small Text)  
2. **Floor (طابق):**  
   * floor\_number (Int, Mandatory)  
   * building (Link, Options: Building, Mandatory)  
3. **Zone (منطقة):**  
   * zone\_name (Data, Mandatory)  
   * floor (Link, Options: Floor, Mandatory)  
   * zone\_type (Select, Options: \\nQuiet\\nCollaborative\\nPrivate Office)  
4. **Bookable Asset (أصل قابل للحجز):**  
   * asset\_name (Data, Mandatory) \- (e.g., "Office-101", "Meeting Room A")  
   * asset\_type (Select, Options: \\nDesk\\nMeeting Room\\nPhone Booth, Mandatory)  
   * location (Link, Options: Zone, Mandatory)  
   * capacity (Int, Default: 1\)  
   * status (Select, Options: \\nAvailable\\nUnder Maintenance, Default: Available)  
5. **Asset Booking (حجز أصل):**  
   * asset (Link, Options: Bookable Asset, Mandatory)  
   * booked\_by (Link, Options: User, Mandatory, Read Only)  
   * company (Link, Options: Company, Mandatory, Read Only)  
   * start\_time (Datetime, Mandatory)  
   * end\_time (Datetime, Mandatory)  
   * **التحقق من الصحة (Validation):** سيتم إضافة Server Script من نوع Before Save للتحقق من عدم وجود حجوزات متداخلة لنفس الأصل.

### **3\. التقنيات والمكتبات الرئيسية**

* **Frappe Framework:** Custom App, DocType, Server Script (Validation).  
* **Python:** منطق التحقق من تداخل التواريخ.

### **4\. معايير القبول**

* يجب أن يتمكن المسؤولون من تعريف المباني والطوابق والمناطق والأصول القابلة للحجز من خلال واجهة Desk.  
* يجب أن يتمكن المستخدمون من إنشاء سجل Asset Booking جديد.  
* يجب أن يمنع النظام إنشاء حجز جديد إذا كان يتعارض مع حجز موجود لنفس الأصل.  
* يجب أن تكون جميع DocTypes مترابطة بشكل صحيح (على سبيل المثال، لا يمكن اختيار منطقة إلا بعد اختيار طابق).

### **5\. المخاطر المحتملة والتخفيف منها**

* **الخطر:** منطق التحقق من تداخل الحجوزات قد يكون معقدًا ويغفل بعض الحالات الهامشية (edge cases).  
  * **التخفيف:** يجب كتابة اختبارات وحدة (Unit Tests) شاملة لمنطق التحقق من الصحة لتغطية جميع السيناريوهات الممكنة (حجز داخل حجز، حجز يغطي حجزًا، إلخ).