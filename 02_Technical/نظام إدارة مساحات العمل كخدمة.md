

# **بنية نظام متكامل لإدارة مساحة العمل متعددة المستأجرين في Arkan Labs**

## **الملخص التنفيذي**

يقدم هذا التقرير مخططًا معماريًا شاملًا لتصميم وتنفيذ نظام إدارة متكامل وموحد لمساحة العمل المغلقة متعددة المستأجرين التابعة لشركة Arkan Labs. يهدف النظام المقترح إلى خدمة كل من فريق الإنتاج التقني الداخلي والفرق الخارجية التي يتم توظيفها لصالح عملاء من المملكة العربية السعودية ومصر. يستند الحل المقترح إلى منظومة Frappe Framework ومنتجاتها مفتوحة المصدر (ERPNext, Frappe HR, Frappe Helpdesk)، لتكون بمثابة العمود الفقري الرقمي الذي يربط بين الأفراد (الموظفين)، والأماكن (المرافق المادية)، والعمليات (الإدارة التجارية والتشغيلية) ضمن منصة مركزية واحدة.

يسلط الملخص الضوء على الأثر التحولي لهذا النظام على الكفاءة التشغيلية، وسلامة البيانات، والأمن، وجودة تقديم الخدمات لكل من Arkan Labs وعملائها. من خلال إنشاء "مصدر وحيد للحقيقة" (Single Source of Truth)، يقوم النظام بأتمتة العمليات الحيوية بدءًا من إلحاق الموظفين الجدد، مرورًا بإدارة الوصول المادي والمنطقي، وانتهاءً بإصدار الفواتير المعقدة القائمة على الاستخدام. إن هذا الاستثمار لا يمثل مجرد تحديث تقني، بل هو تأسيس لمنصة تشغيلية استراتيجية تمنح Arkan Labs ميزة تنافسية مستدامة في سوق مساحات العمل التقنية المُدارة.

---

## **القسم 1: البنية التحتية الأساسية: منظومة Frappe كعمود فقري رقمي**

يؤسس هذا القسم للأساس المنطقي الاستراتيجي والتقني لاختيار Frappe Framework وERPNext كمنصة أساسية. سيفصّل هذا القسم إعدادات البنية متعددة المستأجرين، التي تُعد حجر الزاوية للنظام بأكمله، ويحدد نموذج التحكم في الوصول الذي يضمن الأمان وسلامة البيانات.

### **1.1. الأساس المنطقي لمنصة موحدة ومفتوحة المصدر**

تكمن الحتمية الاستراتيجية في التغلب على التحديات التي تفرضها الأنظمة المنفصلة. إن استخدام برمجيات متفرقة لإدارة الموارد البشرية، وعلاقات العملاء، والمرافق يؤدي حتمًا إلى إنشاء صوامع بيانات (Data Silos) واحتكاكات تشغيلية تعيق الكفاءة. توفر منصة متكاملة مثل ERPNext مصدرًا وحيدًا وموثوقًا للحقيقة، مما يبسط العمليات ويمكّن من إجراء تحليلات قوية متعددة الوظائف.1

لا يُنظر إلى Frappe كتطبيق جاهز فحسب، بل كإطار عمل متكامل لتطبيقات الويب (Full-stack Web Application Framework).2 هذا التمييز جوهري، حيث يوفر الإطار الأدوات اللازمة — مثل أنواع المستندات (DocTypes)، والبرمجة النصية من جانب العميل والخادم، وواجهة برمجة تطبيقات REST API — لبناء الوظائف المخصصة المطلوبة (مثل الفوترة القائمة على الاستخدام، والتكامل مع الأجهزة) التي لا تتوفر في الحلول الجاهزة.

علاوة على ذلك، فإن الطبيعة مفتوحة المصدر لـ Frappe HR وHelpdesk وERPNext تلغي رسوم الترخيص لكل مستخدم، مما يوفر ميزة تكلفة كبيرة، خاصة عند التوسع في عدد الموظفين والوكلاء.3 يمنح هذا النموذج Arkan Labs سيطرة كاملة على بياناتها وبنيتها المعمارية للنظام. إن هذا الاختيار يمثل تحولًا استراتيجيًا من كون الشركة مستهلكًا لمنتجات البرمجيات كخدمة (SaaS) إلى أن تصبح بانيًا لمنصتها التشغيلية الخاصة. فبدلاً من التعامل مع متطلبات فريدة (مثل الفوترة المتغيرة والتكامل مع الأجهزة) كقيود، يمكن للشركة الآن بناء حلول مخصصة. يتطلب هذا جهدًا أوليًا أعلى في التطوير، ولكنه يوفر مرونة لا مثيل لها على المدى الطويل، وتكاليف تشغيل منخفضة عند التوسع، وميزة تنافسية كبيرة من خلال نظام متكامل ومصمم خصيصًا. إنه يحول مركز التكلفة (تراخيص البرمجيات) إلى أصل استراتيجي (المنصة نفسها).

### **1.2. بنية البيانات متعددة المستأجرين: ضمان الفصل الصارم**

الآلية الأساسية لتحقيق تعدد المستأجرين في ERPNext هي من خلال نوع المستند Company. سيتم إنشاء سجل Company جديد لـ Arkan Labs، بالإضافة إلى سجل منفصل لكل شركة عميلة.5 سيتم تكوين Arkan Labs كـ "شركة مجموعة" (Group Company)، مع إنشاء كل شركة عميلة ككيان تابع (Child Company). هذه البنية الهرمية ضرورية لإعداد تقارير مالية موحدة مع الحفاظ على حدود قانونية وتشغيلية منفصلة لكل كيان.5

بطبيعتها، ترتبط المستندات الحركية (مثل فواتير المبيعات وقيود اليومية) والعديد من السجلات الرئيسية (مثل الموظف والأصل) بشركة معينة. هذا يضمن تلقائيًا أن المستخدمين من "العميل أ" لا يمكنهم رؤية البيانات الخاصة بـ "العميل ب".

سيتم تكوين السجلات الرئيسية للموارد البشرية بذكاء. يمكن أن تكون بعض السجلات، مثل Employment Type (نوع التوظيف)، عالمية (مثل "متعاقد لصالح عميل")، بينما يجب أن تكون سجلات أخرى خاصة بالشركة، مثل Holiday List (قائمة العطلات) وLeave Policy (سياسة الإجازات)، لمعالجة القوانين الإقليمية في المملكة العربية السعودية ومصر.5 يتم تعيين

Default Holiday List على مستوى الشركة، مما يفرض هذا الفصل بشكل فعال.5

### **1.3. إطار موحد للمستخدمين والتحكم في الوصول**

سيتم تصميم نموذج قوي للتحكم في الوصول المستند إلى الأدوار (RBAC). يعتمد نظام الأذونات في Frappe على الأدوار المخصصة للمستخدمين، والتي تتحكم في مستويات الوصول (قراءة، كتابة، إنشاء، حذف، إلخ) لكل نوع مستند (DocType).9 سيتم اقتراح مجموعة من الأدوار المخصصة التي تتجاوز الإعدادات الافتراضية:

* **مسؤول Arkan Labs**: وصول على مستوى النظام بالكامل.  
* **مدير شركة العميل**: وصول فقط إلى بيانات شركته (الموظفين، التقارير، المشاريع).  
* **مدير الموارد البشرية في Arkan Labs**: وصول إلى سجلات الموارد البشرية عبر جميع الشركات.  
* **موظف العميل**: وصول للخدمة الذاتية (طلبات الإجازات، قسائم الرواتب) يقتصر على سجله الخاص.  
* **مدير المرافق**: وصول إلى وحدات الأصول والصيانة.

بالإضافة إلى الأدوار، سيتم استخدام "أذونات المستخدم" (User Permissions) لتقييد الوصول بشكل أكبر بناءً على مستندات أو قيم محددة، مثل السماح لـ "مدير شركة العميل" برؤية الموظفين المرتبطين بشركته فقط.6

#### **جدول: مصفوفة التحكم في الوصول المستند إلى الأدوار (RBAC)**

يوضح الجدول التالي مخططًا تفصيليًا للأذونات المقترحة. هذه المصفوفة هي المخطط الأساسي لتكوين أمان النظام، مما يضمن تنفيذ السياسات الأمنية بدقة ويمنع تسرب البيانات بين المستأجرين.

| الدور (Role) | شركة (Company) | موظف (Employee) | فاتورة مبيعات (Sales Invoice) | مشروع (Project) | أصل (Asset) | طلب إجازة (Leave Application) |
| ----: | ----: | ----: | ----: | ----: | ----: | ----: |
| **مسؤول Arkan Labs** | قراءة، كتابة، إنشاء، حذف | قراءة، كتابة، إنشاء، حذف | قراءة، كتابة، إنشاء، حذف | قراءة، كتابة، إنشاء، حذف | قراءة، كتابة، إنشاء، حذف | قراءة، كتابة، إنشاء، حذف |
| **مدير شركة العميل** | قراءة (بشرط: Company \= شركة المستخدم) | قراءة، كتابة، إنشاء (بشرط: Company \= شركة المستخدم) | قراءة (بشرط: Customer \= شركة المستخدم) | قراءة، كتابة (بشرط: Customer \= شركة المستخدم) | قراءة (بشرط: Company \= شركة المستخدم) | قراءة، موافقة (بشرط: Company \= شركة المستخدم) |
| **مدير موارد بشرية Arkan Labs** | قراءة | قراءة، كتابة، إنشاء، حذف | وصول مقيد | وصول مقيد | وصول مقيد | قراءة، كتابة، إنشاء، حذف |
| **موظف العميل** | لا وصول | قراءة (سجله الخاص فقط) | لا وصول | لا وصول | لا وصول | إنشاء، قراءة (طلباته الخاصة فقط) |
| **مدير المرافق** | لا وصول | لا وصول | لا وصول | لا وصول | قراءة، كتابة، إنشاء، حذف | لا وصول |

---

## **القسم 2: إدارة رأس المال البشري: استراتيجية متعددة الشركات للموارد البشرية والرواتب**

يفصل هذا القسم تكوين وحدة الموارد البشرية لتعمل كنواة للنظام، حيث تدير مجموعات متميزة من الموظفين لكيانات قانونية ودول مختلفة، وتعمل بفعالية كـ "صاحب عمل مسجل" (Employer of Record).

### **2.1. إدارة دورة حياة الموظف الكاملة**

يقوم Frappe HR بمركزية جميع بيانات الموظفين في نوع مستند واحد هو Employee، والذي يغطي المعلومات الشخصية، والتاريخ الوظيفي، والراتب، وبيانات الأداء.3 سيتم ربط كل سجل موظف بشكل إلزامي بشركة (

Company) لضمان فصل البيانات. سيتم استخدام أدوات إدارة دورة الحياة في النظام لإنشاء قوائم تحقق موحدة ولكن خاصة بكل شركة لعمليات الإلحاق (مثل توقيع العقود وتخصيص المعدات) ومقابلات الخروج والعمليات المرتبطة بها.3

سيتم تكوين دورات التقييم، ومجالات النتائج الرئيسية (KRAs)، وتتبع الأهداف، والتي يمكن تكييفها لتناسب مقاييس الأداء الداخلية لـ Arkan Labs مقابل أهداف المشاريع الخاصة بالعملاء.3

### **2.2. الرواتب المنفصلة والامتثال الإقليمي (السعودية ومصر)**

يكمن جوهر الامتثال الإقليمي في إنشاء سياسات متميزة لكل Company. سيتم إنشاء وثائق Leave Policy منفصلة للكيانات في السعودية ومصر، لتعكس العطلات الرسمية وقواعد استحقاق الإجازات الفريدة لكل منهما.8 ستتم إدارة الرواتب عن طريق إنشاء قوالب

Salary Structure مختلفة لكل بلد. ستشمل هذه القوالب الإيرادات والخصومات الخاصة بالقوانين المحلية (مثل التأمينات الاجتماعية في السعودية ومصر).3 سيتم تكوين شرائح ضريبة الدخل لكل شركة/دولة.10 إن قدرة النظام على التعامل مع الرواتب متعددة العملات أمر بالغ الأهمية، مما يسمح بمعالجة الرواتب بالريال السعودي والجنيه المصري، مع إمكانية توحيد التقارير بعملة أساسية مثل الدولار الأمريكي.10

### **2.3. تنظيم نموذج صاحب العمل المسجل (EOR)**

يعرّف نموذج EOR بأن Arkan Labs تعمل كصاحب عمل قانوني للفرق المعينة لصالح عملائها. هذا يعني أن Arkan Labs مسؤولة قانونيًا عن الرواتب والضرائب والمزايا والامتثال لقوانين العمل المحلية.12 في النظام، الموظف الذي يعمل لصالح "العميل أ" سيتم تعيين حقل

Company الخاص به إلى "العميل أ (شركة تابعة لـ Arkan Labs)". ومع ذلك، ستتم إدارة عقد عمله ومعالجة راتبه وامتثاله القانوني بالكامل من قبل فريق الموارد البشرية في Arkan Labs باستخدام أدوات النظام.

للتمييز بين الموظفين، سيتم إضافة حقل مخصص، Employee Category (فئة الموظف)، إلى نوع مستند Employee مع خيارات مثل "داخلي في Arkan Labs" و"مدار من قبل العميل". سيكون هذا الحقل حاسمًا لإعداد التقارير والتصفية وتطبيق سياسات أو مسارات عمل داخلية مختلفة.

إن وحدة الموارد البشرية هنا لا تعمل كأداة إدارية فحسب، بل تتحول إلى قاعدة بيانات مركزية لإدارة الهوية والوصول (IAM) للمساحة المادية والرقمية بأكملها. حالة الموظف في Frappe HR هي المصدر النهائي للحقيقة. فبدلاً من التزويد اليدوي للوصول في أنظمة منفصلة لكل موظف جديد أو مغادر، وهو أمر غير فعال ويمثل خطرًا أمنيًا كبيرًا، يمكن بناء مسارات عمل آلية. هذه المسارات، التي سيتم تفصيلها في القسم 5، يتم تشغيلها بناءً على تغييرات حالة الموظف (مثل إكمال Onboarding، أو الموافقة على Leave Application، أو Employee Separation). يمكن لهذه المشغلات أن تقوم برمجيًا بمنح أو إلغاء الوصول. على سبيل المثال، عملية إنهاء خدمة موظف في نظام الموارد البشرية ستؤدي تلقائيًا إلى إطلاق استدعاءات API لنظام التحكم في الوصول إلى الأبواب لإلغاء تنشيط بطاقته، ولجهاز التحكم في الشبكة لتعطيل وصوله. هذا يحول نظام الموارد البشرية إلى محرك بنية تحتية أمنية مؤتمتة وموحدة.

---

## **القسم 3: إدارة علاقات العملاء والإدارة التجارية**

يركز هذا القسم على دورة حياة العميل بأكملها، بدءًا من الإلحاق وإدارة العقود، وصولًا إلى العملية الحرجة والمطورة خصيصًا للفوترة الآلية القائمة على الاستخدام.

### **3.1. رحلة إلحاق العميل: مسار عمل منظم**

سيتم الاستفادة من Frappe CRM لإدارة مسار المبيعات الأولي، وتتبع العملاء المحتملين والفرص والصفقات.13 بالاعتماد على أفضل الممارسات في SaaS B2B، سيتم تصميم خطة إلحاق منظمة تبدأ بعد توقيع العقد.14 هذه ليست مجرد رسالة ترحيب 16، بل عملية متعددة الخطوات تتم إدارتها داخل النظام:

1. **اجتماع الانطلاق والاستكشاف**: اجتماع انطلاق رسمي لمواءمة الأهداف.15  
2. **إعداد النظام**: إنشاء نوع مستند Company، وتكوين سياسات الموارد البشرية الخاصة بالعميل، وإعداد Contract.  
3. **توفير الفريق**: إلحاق موظفي العميل المعينين في نظام الموارد البشرية تحت شركتهم.  
4. **الانطلاق**: تفعيل الخدمات والوصول المادي ودورات الفوترة.

ستتم إدارة كل عملية إلحاق عميل كمشروع داخلي (Project) في ERPNext، مع مهام وجداول زمنية ومالكين معينين لضمان المساءلة والتسليم السلس من المبيعات إلى العمليات.14

### **3.2. إدارة دورة حياة العقود والاشتراكات**

سيتم استخدام نوع مستند Contract في ERPNext لتخزين الاتفاقية القانونية الرئيسية مع كل عميل. يمكن أن يحتوي على تواريخ البدء والانتهاء، والشروط والأحكام، ويمكن ربطه بجميع المعاملات ذات الصلة (أوامر المبيعات، الفواتير) للحصول على مسار تدقيق كامل.19 بالنسبة للرسوم المتكررة الثابتة (مثل رسوم الإدارة الأساسية)، فإن نوع مستند

Subscription هو الحل المثالي. يمكن تحديد خطط اشتراك مرتبطة بعناصر خدمة محددة، وتعيين فترة الفوترة (على سبيل المثال، شهريًا)، وسيقوم النظام تلقائيًا بإنشاء فواتير المبيعات.20

### **3.3. أتمتة الفوترة المعقدة: مخطط تطوير مخصص**

تمثل الفوترة القائمة على الاستخدام تحديًا، حيث أن وحدة Subscription القياسية مصممة للتجديدات بمبالغ ثابتة، وليس للفوترة المتغيرة (مثل الفوترة لكل مكتب/موظف نشط شهريًا).20 هذه فجوة وظيفية حرجة تتطلب تطويرًا مخصصًا.

**الحل المقترح \- نموذج البيانات:**

1. إنشاء نوع مستند مخصص: Monthly Tenant Usage (استخدام المستأجر الشهري).  
2. الحقول: Client Company (رابط: Company)، Fiscal Month (الشهر المالي)، Fiscal Year (السنة المالية)، Number of Active Employees (عدد الموظفين النشطين)، Additional Services (جدول فرعي للخدمات الإضافية)، Total Billable Amount (إجمالي المبلغ المستحق).

**الحل المقترح \- الأتمتة:**

1. **برنامج نصي مجدول للخادم**: إنشاء برنامج نصي بلغة Python مجدول للتشغيل شهريًا (على سبيل المثال، في اليوم الخامس والعشرين من كل شهر) باستخدام المجدول المدمج في Frappe.22  
2. **منطق البرنامج النصي**:  
   * سيتكرر البرنامج النصي عبر جميع سجلات شركات العملاء النشطة.  
   * لكل شركة، سيستعلم عن نوع مستند Employee لحساب عدد الموظفين النشطين لتلك الفترة.  
   * سينشئ سجل Monthly Tenant Usage جديدًا، ويملؤه بالبيانات المحسوبة.  
   * بعد ذلك، سينشئ برمجيًا مستند Sales Invoice جديدًا في حالة مسودة.24  
   * سيتم ملء بنود Sales Invoice بناءً على البيانات الموجودة في سجل Monthly Tenant Usage والأسعار المحددة في Contract العميل.  
   * يمكن بعد ذلك مراجعة الفاتورة المسودة وتقديمها من قبل الفريق المالي.

يعتمد هذا الحل على قدرات البرمجة النصية من جانب الخادم في Frappe (Python) وواجهة برمجة التطبيقات الموجهة للمستندات (frappe.new\_doc, doc.insert()) لإنشاء مستندات مرتبطة تلقائيًا.24

إن محرك الفوترة المخصص هو القلب التجاري للنظام. دقة وموثوقية هذا المحرك تؤثر بشكل مباشر على إيرادات Arkan Labs وثقة العملاء. إن إدخال نوع مستند وسيط Monthly Tenant Usage هو خطوة حاسمة. فهو يفصل عملية *جمع البيانات* عن *إنشاء الفاتورة*. يعمل هذا المستند الوسيط كسجل واضح وقابل للتدقيق لسبب كون مبلغ الفاتورة كما هو. يمكن عرض هذا السجل للعميل، والذي يسرد بشفافية "X موظفًا بسعر Y"، وما إلى ذلك. هذا التصميم يجعل النظام أكثر قوة، ويسهل تصحيح الأخطاء، ويبني علاقة فوترة شفافة وجديرة بالثقة مع العميل، وهو عامل رئيسي في الاحتفاظ بالعملاء في خدمات B2B.

---

## **القسم 4: إدارة مساحة العمل والمرافق الذكية**

يحدد هذا القسم كيفية إنشاء "توأم رقمي" لمساحة العمل المادية داخل Frappe، مما يتيح الحجز الذكي وإدارة الموارد وتبسيط عمليات الصيانة.

### **4.1. نمذجة البيئة المادية: أنواع مستندات مخصصة**

يفتقر ERPNext القياسي إلى وحدات مخصصة لإدارة المرافق. سيتم نمذجة مساحة العمل باستخدام أنواع مستندات مخصصة، مستوحاة من نماذج بيانات برامج IWMS المخصصة.29 سيتم إنشاء نموذج هرمي:

* Building (مبنى) \-\> Floor (طابق) \-\> Zone (منطقة) (على سبيل المثال، "منطقة هادئة"، "منطقة تعاون").  
* Bookable Asset (أصل قابل للحجز): نوع مستند أساسي لأي شيء يمكن حجزه. ستشمل الحقول Asset Name (اسم الأصل)، Asset Type (نوع الأصل) (مثل مكتب، غرفة اجتماعات)، Location (رابط إلى Zone)، Capacity (السعة)، Status (الحالة).  
* Asset Booking (حجز أصل): نوع مستند حركي لتسجيل الحجوزات. الحقول: Asset (رابط)، Booked By (رابط: User)، Company، Start Time (وقت البدء)، End Time (وقت الانتهاء).

#### **جدول: نموذج أنواع المستندات لإدارة المرافق**

يوفر هذا الجدول بنية بيانات واضحة قبل كتابة أي كود، مما يضمن أن العلاقات بين المساحات المادية والأصول سليمة منطقيًا وتمكّن من بناء وظائف متقدمة مثل المخطط التفاعلي ولوحات المعلومات.

| اسم نوع المستند (DocType) | الحقول الرئيسية (مع النوع) | الغرض / سير العمل |
| ----: | ----: | ----: |
| **Building (مبنى)** | Building Name (Data), Address (Small Text) | يمثل المبنى المادي. المستوى الأعلى في التسلسل الهرمي. |
| **Floor (طابق)** | Floor Number (Int), Building (Link: Building) | يمثل طابقًا داخل مبنى. |
| **Zone (منطقة)** | Zone Name (Data), Floor (Link: Floor), Zone Type (Select) | يقسم الطابق إلى مناطق وظيفية (مثل منطقة هادئة، منطقة تعاون). |
| **Bookable Asset (أصل قابل للحجز)** | Asset Name (Data), Asset Type (Select), Location (Link: Zone), Capacity (Int) | يمثل أي مورد قابل للحجز (مكتب، غرفة اجتماعات، كشك هاتف). |
| **Asset Booking (حجز أصل)** | Asset (Link: Bookable Asset), Booked By (Link: User), Company (Link: Company), Start Time (Datetime), End Time (Datetime) | يسجل حجز أصل من قبل مستخدم لفترة زمنية محددة. |
| **Maintenance Request (طلب صيانة)** | Asset (Link: Bookable Asset), Issue Type (Select), Description (Text), Status (Select) | يمثل طلب صيانة أو خدمة لأصل معين. |

### **4.2. مخطط الطابق التفاعلي ونظام الحجز**

سيتم تطوير صفحة مخصصة "Workspace" داخل Frappe، والتي توفر تجربة مستخدم أكثر ديناميكية من نموذج DocType القياسي.30 سيكون العنصر المركزي هو مخطط طابق تفاعلي بتنسيق SVG، وهو نهج حديث وبديهي لإدارة المساحات.32

* سيكون كل أصل قابل للحجز (مكتب، غرفة) على SVG كائنًا له معرف فريد.  
* ستتعامل JavaScript على الصفحة المخصصة مع أحداث النقر على هذه الكائنات.  
* سيقوم استدعاء frappe.call (AJAX) في الخلفية بجلب حالة الحجز في الوقت الفعلي للأصل من نوع مستند Asset Booking.31  
* سيتم تحديث لون كائن SVG ديناميكيًا (على سبيل المثال، أخضر للمتاح، أحمر للمحجوز).  
* سيؤدي النقر على أصل متاح إلى فتح مربع حوار للحجز.

لعرض أكثر تقليدية، يمكن تنفيذ تقويم موارد باستخدام مكتبات JavaScript مثل DayPilot، والذي يعرض الأصول كأعمدة والوقت كصفوف، مما يوفر نظرة عامة واضحة على التوفر.33

### **4.3. عمليات الدعم والصيانة الموحدة**

سيتم تكوين Frappe Helpdesk كنقطة مركزية لجميع طلبات الدعم—سواء كان كرسيًا مكسورًا، أو مشكلة في تكنولوجيا المعلومات، أو طلب خدمة.4 هذا يركز الاتصالات ويمنع ضياع الطلبات في البريد الإلكتروني. الميزة الرئيسية هي القدرة على تحديد اتفاقيات مستوى الخدمة (SLAs) لأوقات الاستجابة والحل.4 سيتم إنشاء سياسات SLA مختلفة واستخدام شروط التعيين لتطبيقها بناءً على نوع الطلب أو الشركة العميلة التي قدمت الطلب.36 سيتم تكوين قواعد التعيين (Assignment Rules) لتوجيه التذاكر تلقائيًا إلى الفريق الصحيح (مثل "المرافق"، "دعم تكنولوجيا المعلومات") بناءً على فئة التذكرة، مما يضمن التعامل الفعال.37

إن المخطط التفاعلي للطابق هو أكثر من مجرد أداة حجز؛ إنه طبقة تصور بيانات تدفع الذكاء التشغيلي وتحسين المساحات. على الرغم من أن المتطلب الأولي هو حجز المكاتب والغرف، إلا أن نموذج البيانات الأساسي يتتبع كل حجز: من، ماذا، متى، ولأي مدة، ومن أي شركة. يمكن تجميع بيانات الحجز هذه بمرور الوقت. من خلال ربط هذه البيانات بأدوات إعداد التقارير في Frappe، يمكن بناء لوحات معلومات تجيب على أسئلة عمل حاسمة مثل: "ما هو معدل الاستخدام الأقصى لغرف الاجتماعات لدينا؟" أو "أي شركة عميلة تستخدم معظم المكاتب المشتركة؟". هذا يحول مخطط الطابق من أداة تشغيلية بسيطة إلى أداة استراتيجية، ويوفر تحليلات البيانات 39 اللازمة لاتخاذ قرارات قائمة على البيانات حول إدارة المرافق، والتوسع المستقبلي، وحتى نماذج التسعير.

---

## **القسم 5: البنية التحتية التكنولوجية الآمنة والتحكم المتكامل في الوصول**

يفصل هذا القسم البنية التحتية الحيوية التي تدعم العملية بأكملها، مع التركيز على فصل الشبكات والتكامل السلس والمؤتمت للتحكم في الوصول المادي للأبواب مع نظام الموارد البشرية الأساسي.

### **5.1. مخطط بنية الشبكة: تصميم متعدد الشبكات الافتراضية (VLAN)**

لتلبية متطلبات الأمان متعددة المستأجرين، يجب أن يكون كل مستأجر (Arkan Labs، العميل أ، العميل ب، إلخ) على شبكة منفصلة منطقيًا. تعد الشبكات المحلية الافتراضية (VLANs) هي التقنية القياسية لتحقيق هذا الفصل.40 سيتم استخدام أجهزة من فئة المؤسسات مثل Ubiquiti UniFi. سيتم إنشاء VLAN مخصص لكل شركة مستأجرة، بالإضافة إلى شبكات VLAN إضافية للإدارة والضيوف.41

* VLAN 10: شبكة Arkan Labs المؤسسية  
* VLAN 20: شبكة العميل أ المؤسسية  
* VLAN 30: شبكة العميل ب المؤسسية  
* VLAN 99: شبكة الضيوف (مع عزل العملاء وحدود النطاق الترددي)  
* VLAN 100: إدارة الشبكة

بشكل حاسم، سيتم تكوين قواعد جدار الحماية على البوابة لحظر كل حركة المرور بين الشبكات الافتراضية بشكل افتراضي، باستثناء الخدمات المسموح بها بشكل صريح ومحدد (على سبيل المثال، السماح لجميع شبكات VLAN المؤسسية بالوصول إلى طابعة مشتركة على عنوان IP معين).40 سيتم تعيين VLAN لكل مستأجر إلى SSID واي فاي مخصص (مثل "ArkanLabs\_Corp"، "ClientA\_Corp") وتعيينه إلى منافذ محول فعلية محددة في منطقة مكتبهم المخصصة.41

#### **جدول: ملخص تكوين VLAN وسياسة جدار الحماية**

يعمل هذا الجدول كدليل تكوين مباشر لمسؤول الشبكة، ويوثق صراحة سياسة العزل، ويشكل أساس الموقف الأمني للشبكة.

| معرف VLAN | اسم الشبكة | الشبكة الفرعية (Subnet) | نطاق DHCP | SSIDs المعينة | قواعد جدار الحماية الرئيسية |
| ----: | ----: | ----: | ----: | ----: | ----: |
| **10** | Arkan Labs Corporate | 192.168.10.0/24 | 192.168.10.100−200 | ArkanLabs\_Corp | السماح بالوصول إلى VLAN 100\. رفض الكل إلى VLAN 20, 30, 99\. |
| **20** | Client A Corporate | 192.168.20.0/24 | 192.168.20.100−200 | ClientA\_Corp | السماح بالوصول إلى VLAN 100\. رفض الكل إلى VLAN 10, 30, 99\. |
| **30** | Client B Corporate | 192.168.30.0/24 | 192.168.30.100−200 | ClientB\_Corp | السماح بالوصول إلى VLAN 100\. رفض الكل إلى VLAN 10, 20, 99\. |
| **99** | Guest Network | 192.168.99.0/24 | 192.168.99.100−200 | ArkanLabs\_Guest | تمكين عزل العميل. رفض الكل إلى VLAN 10, 20, 30, 100\. |
| **100** | Management | 192.168.100.0/24 | ثابت | (لا يوجد) | السماح بالوصول من VLAN 10, 20, 30\. رفض الكل إلى VLAN 99\. |

### **5.2. التحكم في الوصول المادي الموجه بواجهة برمجة التطبيقات (API)**

يجب اختيار نظام تحكم في الوصول حديث يعتمد على واجهة برمجة التطبيقات أولاً. الأنظمة القديمة غالبًا ما تكون مغلقة ويصعب تكاملها. أنظمة مثل HID (مع واجهات برمجة التطبيقات Origo وOPIN)، أو Rhombus، أو ProdataKey مصممة لهذا النوع من التحكم البرمجي.42 توفر منصة HID Origo واجهة برمجة تطبيقات REST شاملة لإدارة دورة حياة الوصول بأكملها.45 تشمل قدرات واجهة برمجة التطبيقات الرئيسية ما يلي:

* **إدارة المستخدمين**: إنشاء وتحديث وحذف المستخدمين.48  
* **إدارة بيانات الاعتماد**: إصدار وإلغاء بيانات الاعتماد (مثل الهويات المحمولة أو البطاقات المادية) لمستخدم معين.50

سيلتزم تكامل واجهة برمجة التطبيقات بأفضل ممارسات الأمان، مما يضمن أن نظام Frappe لديه فقط الحد الأدنى من الأذونات اللازمة لأداء وظائفه.51

### **5.3. سير عمل توفير وإلغاء توفير الوصول "بدون لمس"**

الهدف هو أتمتة منح وإلغاء الوصول المادي والشبكي بالكامل بناءً على حالة الموظف في نظام Frappe HR.

**سير عمل التوفير (عند الإلحاق):**

1. يكمل مدير الموارد البشرية عملية إلحاق Employee في Frappe HR وتصبح حالة الموظف "نشط".  
2. يؤدي هذا إلى تشغيل خطاف برمجي نصي من جانب الخادم on\_submit على نوع مستند Employee.  
3. يقوم البرنامج النصي بلغة Python بإجراء استدعاء واجهة برمجة تطبيقات REST إلى HID Origo API لإنشاء مستخدم جديد، وتمرير اسم الموظف وبريده الإلكتروني.48  
4. يتم إجراء استدعاء ثانٍ لواجهة برمجة التطبيقات لإصدار بيانات اعتماد محمولة جديدة لذلك المستخدم.49 يتلقى المستخدم بريدًا إلكترونيًا لإعداد مفتاحه المحمول.  
5. في الوقت نفسه، يمكن للبرنامج النصي تحديث سمة خادم RADIUS لتعيين جهاز المستخدم (عبر عنوان MAC) إلى VLAN الشركة الصحيح عند الاتصال بالشبكة.41

**سير عمل إلغاء التوفير (عند إنهاء الخدمة):**

1. يقوم مدير الموارد البشرية بمعالجة Employee Separation في Frappe، وتغيير حالة Employee إلى "غير نشط".  
2. يؤدي هذا إلى تشغيل خطاف برمجي نصي آخر on\_submit.  
3. يقوم البرنامج النصي بإجراء استدعاء واجهة برمجة تطبيقات REST إلى HID Origo API لإلغاء جميع بيانات الاعتماد المرتبطة بمعرف المستخدم هذا.50 يتم قطع وصوله المادي على الفور.  
4. تتم إزالة سمة خادم RADIUS، مما يمنع وصوله إلى الشبكة.

إن تكامل الموارد البشرية مع التحكم في الوصول المادي والشبكي يخلق نسيجًا أمنيًا موحدًا يقلل بشكل كبير من التهديدات الداخلية والنفقات التشغيلية. إحدى نقاط الضعف الأمنية الرئيسية في أي منظمة هي مشكلة "بقاء الوصول" — عندما تظل بيانات اعتماد الموظف الذي تم إنهاء خدمته نشطة لساعات أو أيام. عادة ما يكون هذا بسبب الاتصال اليدوي البطيء بين إدارات الموارد البشرية وتكنولوجيا المعلومات والمرافق. يلغي سير العمل "بدون لمس" المقترح فجوة الاتصال هذه تمامًا. المشغل هو حدث النظام في مصدر الحقيقة الوحيد (سجل الموارد البشرية). والإجراء هو استدعاء API فوري من آلة إلى آلة. يتم تقليل الفترة الزمنية التي يمكن لموظف سابق ساخط أن يسبب فيها ضررًا من أيام إلى ثوانٍ. علاوة على ذلك، توفر هذه الأتمتة وقتًا كبيرًا لموظفي الموارد البشرية وتكنولوجيا المعلومات، الذين لم يعودوا مضطرين لإدارة قوائم التحكم في الوصول يدويًا في أنظمة متعددة.

---

## **القسم 6: خارطة طريق التنفيذ والتوصيات الاستراتيجية**

يقدم هذا القسم الأخير نهجًا عمليًا ومرحليًا لبناء ونشر هذا النظام المعقد، ويسلط الضوء على مهام التطوير الحرجة ويقدم نصائح استراتيجية للنجاح على المدى الطويل.

### **6.1. استراتيجية النشر المرحلي**

* **المرحلة الأولى: إعداد النظام الأساسي والإطلاق الداخلي (الأشهر 1-3):**  
  * نشر Frappe/ERPNext على خادم إنتاج.2  
  * تكوين الهيكل الأساسي متعدد الشركات مع Arkan Labs ككيان أول.  
  * إعداد وترحيل جميع موظفي Arkan Labs الداخليين إلى Frappe HR.  
  * تكوين وإطلاق عمليات الموارد البشرية الداخلية: الإجازات، الحضور، الرواتب.3  
  * تكوين Frappe Helpdesk لإصدار التذاكر الداخلية لتكنولوجيا المعلومات/المرافق.4  
* **المرحلة الثانية: إلحاق أول عميل وتطوير الفوترة المخصصة (الأشهر 4-6):**  
  * إلحاق أول شركة عميلة تجريبية، وتكوين سياسات الموارد البشرية والموظفين الخاصة بها.  
  * تطوير واختبار نوع المستند المخصص Monthly Tenant Usage والبرنامج النصي المجدول للخادم لإنشاء الفواتير تلقائيًا.22  
  * تشغيل الفوترة الموازية لدورة واحدة للتحقق من الدقة قبل التحول الكامل.  
* **المرحلة الثالثة: إدارة مساحة العمل وتكامل التحكم في الوصول (الأشهر 7-9):**  
  * تطوير أنواع المستندات المخصصة لإدارة المرافق (Bookable Asset، إلخ).  
  * بناء صفحة مخصصة لمخطط الطابق التفاعلي SVG.30  
  * اختيار وشراء وتركيب أجهزة التحكم في الوصول الموجهة بواجهة برمجة التطبيقات.  
  * تطوير واختبار البرامج النصية للخادم "بدون لمس" للتوفير/إلغاء التوفير التي تدمج Frappe HR مع واجهة برمجة تطبيقات التحكم في الوصول.48  
* **المرحلة الرابعة: الإطلاق الكامل والتحسين (الأشهر 10-12):**  
  * إلحاق جميع شركات العملاء المتبقية.  
  * نشر نظام التحكم في الوصول المتكامل عبر المرفق بأكمله.  
  * تطوير لوحات معلومات وتقارير تحليلية متقدمة.  
  * جمع ملاحظات المستخدمين وبدء الدورة الأولى من تحسينات النظام.

### **6.2. التخصيصات الحرجة على المسار**

يسرد هذا القسم الفرعي ويؤكد مجددًا على مهام التطوير الرئيسية التي ليست ميزات جاهزة وهي ضرورية للنظام لتلبية المتطلبات:

1. **محرك الفوترة القائم على الاستخدام**: البرنامج النصي المجدول الشهري لحساب الاستخدام وإنشاء الفواتير.  
2. **تكامل التحكم في الوصول**: البرامج النصية من جانب الخادم لاستدعاء واجهة برمجة تطبيقات التحكم في الوصول المادي بناءً على أحداث الموارد البشرية.  
3. **وحدة إدارة المرافق**: مجموعة أنواع المستندات المخصصة لنمذجة المساحة المادية.  
4. **مخطط الطابق التفاعلي**: صفحة Frappe المخصصة مع SVG وJavaScript للحجز.

### **6.3. الحوكمة وقابلية التوسع**

يجب على Arkan Labs التخطيط للتطوير والصيانة المستمرين. هذا يعني إما توظيف مطوري Frappe داخليين أو إنشاء عقد استشاري مع وكالة شريكة معتمدة من Frappe.1 يجب وضع سياسات واضحة لإدخال البيانات، وتعيين أدوار المستخدمين، ومراجعة البيانات بانتظام للحفاظ على سلامة "مصدر الحقيقة الوحيد". يمكن أن يكون النشر الأولي على خادم واحد، ولكن مع نمو عدد المستخدمين والمعاملات، يمكن توسيع البنية (على سبيل المثال، خادم قاعدة بيانات منفصل، وعمليات عاملة للمهام الخلفية).

## **الخاتمة**

هذه البنية المقترحة ليست مجرد ترقية لتكنولوجيا المعلومات؛ إنها المنصة التأسيسية لنموذج تقديم الخدمة بأكمله في Arkan Labs. إنها توفر بيئة قوية وآمنة ومؤتمتة للغاية تمكّن من التميز التشغيلي، وتعزز ثقة العملاء من خلال الشفافية، وتخلق أساسًا قابلاً للتطوير للنمو المستقبلي. من خلال الاستثمار في هذه المنصة الموحدة، ستمتلك Arkan Labs ميزة تنافسية كبيرة ومستدامة في سوق مساحات العمل التقنية المُدارة.

#### **Works cited**

1. Employee and Payroll Management with ERPNext: A Complete Guide, accessed September 13, 2025, [https://nexeves.com/blog/ERPNext/employee-and-payroll-management-with-erpnext-a-complete-guide](https://nexeves.com/blog/ERPNext/employee-and-payroll-management-with-erpnext-a-complete-guide)  
2. frappe/erpnext: Free and Open Source Enterprise Resource Planning (ERP) \- GitHub, accessed September 13, 2025, [https://github.com/frappe/erpnext](https://github.com/frappe/erpnext)  
3. Frappe HR \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/hr/introduction](https://docs.frappe.io/hr/introduction)  
4. Open Source Support Ticketing System | Frappe Helpdesk, accessed September 13, 2025, [https://frappe.io/helpdesk](https://frappe.io/helpdesk)  
5. Company Setup \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/erpnext/user/manual/en/company-setup](https://docs.frappe.io/erpnext/user/manual/en/company-setup)  
6. Multi-company setup in ERPNext/Frappe \- YouTube, accessed September 13, 2025, [https://www.youtube.com/watch?v=aHtg-DqsRv4](https://www.youtube.com/watch?v=aHtg-DqsRv4)  
7. Human Resource Setup \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/hr/human-resource-setup](https://docs.frappe.io/hr/human-resource-setup)  
8. ERPNext Frappe HR: Basic Setup Steps \- CitrusLeaf | Blog, accessed September 13, 2025, [https://citrusleaf.in/blog/setting-up-hrms-module-erpnext/](https://citrusleaf.in/blog/setting-up-hrms-module-erpnext/)  
9. How to manage your companies for free with ERPNext | by Antonio Cañada | Medium, accessed September 13, 2025, [https://tonicanada.medium.com/how-to-manage-your-companies-for-free-with-erpnext-858fa7e4f62f](https://tonicanada.medium.com/how-to-manage-your-companies-for-free-with-erpnext-858fa7e4f62f)  
10. ERPNext HR & Payroll Solutions \- Sigzen Technologies, accessed September 13, 2025, [https://www.sigzen.com/erpnext/hr-payroll/](https://www.sigzen.com/erpnext/hr-payroll/)  
11. Leave Management \- Frappe, accessed September 13, 2025, [https://frappe.io/hr/leave-management](https://frappe.io/hr/leave-management)  
12. What is an Employer of Record (EOR)? | HR & Payroll Glossary | Paylocity, accessed September 13, 2025, [https://www.paylocity.com/resources/glossary/eor/](https://www.paylocity.com/resources/glossary/eor/)  
13. Frappe Crm \- Tridots Tech, accessed September 13, 2025, [https://beta-tridotstech.frappe.cloud/frappe-crm](https://beta-tridotstech.frappe.cloud/frappe-crm)  
14. A Guide to B2B SaaS Customer Onboarding, accessed September 13, 2025, [https://arrows.to/guide/onboarding-101](https://arrows.to/guide/onboarding-101)  
15. SaaS Customer Onboarding Guide: Best Practices & Templates \- Dock.us, accessed September 13, 2025, [https://www.dock.us/library/customer-onboarding](https://www.dock.us/library/customer-onboarding)  
16. Customer onboarding guide: 11 templates \+ best practices, accessed September 13, 2025, [https://www.zendesk.com/blog/customer-onboarding/](https://www.zendesk.com/blog/customer-onboarding/)  
17. 16 Customer Onboarding Best Practices For SaaS | by Userpilot Team | Medium, accessed September 13, 2025, [https://medium.com/@userpilot/16-customer-onboarding-best-practices-for-saas-e95a6f2002bb](https://medium.com/@userpilot/16-customer-onboarding-best-practices-for-saas-e95a6f2002bb)  
18. B2B SaaS customer onboarding: Guide to a 7-step process | Moxo, accessed September 13, 2025, [https://www.moxo.com/blog/b2b-saas-customer-client-onboarding](https://www.moxo.com/blog/b2b-saas-customer-client-onboarding)  
19. Contract \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/erpnext/user/manual/en/contract](https://docs.frappe.io/erpnext/user/manual/en/contract)  
20. Subscription \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/erpnext/user/manual/en/subscription](https://docs.frappe.io/erpnext/user/manual/en/subscription)  
21. How To Manage Subscriptions With Erpnext, accessed September 13, 2025, [https://multisaber.angolaerp.co.ao/docs/user/manual/en/accounts/articles/how-to-manage-subscriptions-with-erpnext](https://multisaber.angolaerp.co.ao/docs/user/manual/en/accounts/articles/how-to-manage-subscriptions-with-erpnext)  
22. Mastering ERPNext: Creating Custom Schedulers for Automated Task Management in Your App \- YouTube, accessed September 13, 2025, [https://www.youtube.com/watch?v=DBMW6sfHx78](https://www.youtube.com/watch?v=DBMW6sfHx78)  
23. ERPNext/Frappe Framework : Schedulers and Automating Tasks \- YouTube, accessed September 13, 2025, [https://www.youtube.com/watch?v=8\_KIilBQdZE](https://www.youtube.com/watch?v=8_KIilBQdZE)  
24. I want to create sales invoice document automatically on the basis on other doctype, accessed September 13, 2025, [https://discuss.frappe.io/t/i-want-to-create-sales-invoice-document-automatically-on-the-basis-on-other-doctype/118923](https://discuss.frappe.io/t/i-want-to-create-sales-invoice-document-automatically-on-the-basis-on-other-doctype/118923)  
25. Creating Sales Invoices Programmatically \- Integration \- Frappe Forum, accessed September 13, 2025, [https://discuss.frappe.io/t/creating-sales-invoices-programmatically/20562](https://discuss.frappe.io/t/creating-sales-invoices-programmatically/20562)  
26. Automatically Create Invoice and Payment while creating order \- Frappe Forum, accessed September 13, 2025, [https://discuss.frappe.io/t/automatically-create-invoice-and-payment-while-creating-order/75701](https://discuss.frappe.io/t/automatically-create-invoice-and-payment-while-creating-order/75701)  
27. Custom Scripts, accessed September 13, 2025, [https://manualpt.angolaerp.co.ao/docs/user/manual/en/customize-erpnext/custom-scripts](https://manualpt.angolaerp.co.ao/docs/user/manual/en/customize-erpnext/custom-scripts)  
28. Populate Data From One DocType To Another Using frappe.new\_doc | Frappe | ERPNext, accessed September 13, 2025, [https://www.youtube.com/watch?v=bQLfKHxgqYo](https://www.youtube.com/watch?v=bQLfKHxgqYo)  
29. Facility Management Software Solutions | FM:Systems, accessed September 13, 2025, [https://fmsystems.com/products/facility-management-software/](https://fmsystems.com/products/facility-management-software/)  
30. Create custom page \- Frappe Forum, accessed September 13, 2025, [https://discuss.frappe.io/t/create-custom-page/55439](https://discuss.frappe.io/t/create-custom-page/55439)  
31. Creating a new page in ERPNext \- Credence Analytics, accessed September 13, 2025, [https://erp.credenceanalytics.com/erp-development/create-new-page](https://erp.credenceanalytics.com/erp-development/create-new-page)  
32. Interactive svg floorplan \- CodeSandbox, accessed September 13, 2025, [https://codesandbox.io/s/interactive-svg-floorplan-qpp2x](https://codesandbox.io/s/interactive-svg-floorplan-qpp2x)  
33. JavaScript Resource Calendar | DayPilot for JavaScript \- Calendar, Scheduler and Gantt Chart Web Components, accessed September 13, 2025, [https://javascript.daypilot.org/calendar/resource-calendar/](https://javascript.daypilot.org/calendar/resource-calendar/)  
34. Frappe Helpdesk \- LavaLoon, accessed September 13, 2025, [https://lavaloon.com/frappe-helpdesk](https://lavaloon.com/frappe-helpdesk)  
35. Helpdesk \- Frappe Cloud Marketplace, accessed September 13, 2025, [https://bizops.id/marketplace/apps/helpdesk](https://bizops.id/marketplace/apps/helpdesk)  
36. Service Level Agreement \- Frappe, accessed September 13, 2025, [https://docs.frappe.io/helpdesk/service-level-agreement](https://docs.frappe.io/helpdesk/service-level-agreement)  
37. Assignment Rule \- Documentation for Frappe Apps, accessed September 13, 2025, [https://docs.frappe.io/erpnext/user/manual/en/assignment-rule](https://docs.frappe.io/erpnext/user/manual/en/assignment-rule)  
38. Automation \- ERPNext Documentation, accessed September 13, 2025, [https://manualpt.angolaerp.co.ao/docs/user/manual/en/automation](https://manualpt.angolaerp.co.ao/docs/user/manual/en/automation)  
39. How to use data analytics in facility management \- Infraspeak Blog, accessed September 13, 2025, [https://blog.infraspeak.com/data-analytics-in-facility-management/](https://blog.infraspeak.com/data-analytics-in-facility-management/)  
40. Multi-Tenant Office Setup \- VLANs \- Ubiquiti Community, accessed September 13, 2025, [https://community.ui.com/questions/Multi-Tenant-Office-Setup-VLANs/18ca6879-f053-4d5a-b1f3-d0bb85c94d73](https://community.ui.com/questions/Multi-Tenant-Office-Setup-VLANs/18ca6879-f053-4d5a-b1f3-d0bb85c94d73)  
41. Creating Virtual Networks (VLANs) – Ubiquiti Help Center, accessed September 13, 2025, [https://help.ui.com/hc/en-us/articles/9761080275607-Creating-Virtual-Networks-VLANs](https://help.ui.com/hc/en-us/articles/9761080275607-Creating-Virtual-Networks-VLANs)  
42. Door Access Control Systems for Enhanced Security | Rhombus, accessed September 13, 2025, [https://www.rhombus.com/access-control/](https://www.rhombus.com/access-control/)  
43. ProdataKey \- Cloud-Based Access Control & Security Solutions, accessed September 13, 2025, [https://www.prodatakey.com/](https://www.prodatakey.com/)  
44. Physical & Digital Security Integrations | HID Integration Service, accessed September 13, 2025, [https://www.hidglobal.com/solutions/hid-integration-service](https://www.hidglobal.com/solutions/hid-integration-service)  
45. Keep Object HID Origo Model, accessed September 13, 2025, [https://apidocs.feenics.com/hid-origo/](https://apidocs.feenics.com/hid-origo/)  
46. HID Mobile Access® Solutions Datasheet, accessed September 13, 2025, [https://media.howard.com/docs/downloads/HID-mobile-access-solution.pdf](https://media.howard.com/docs/downloads/HID-mobile-access-solution.pdf)  
47. HID Origo API Documentation \- HID Global, accessed September 13, 2025, [https://doc.origo.hidglobal.com/api/](https://doc.origo.hidglobal.com/api/)  
48. User Management \- HID Origo API Documentation, accessed September 13, 2025, [https://doc.origo.hidglobal.com/api/user-management/](https://doc.origo.hidglobal.com/api/user-management/)  
49. Mobile Identities v2.2 \- HID Origo API Documentation, accessed September 13, 2025, [https://doc.origo.hidglobal.com/api/mobile-identities/](https://doc.origo.hidglobal.com/api/mobile-identities/)  
50. Credential Management \- HID Origo API Documentation, accessed September 13, 2025, [https://doc.origo.hidglobal.com/api/credential-management/](https://doc.origo.hidglobal.com/api/credential-management/)  
51. REST API Security: 4 Design Principles and 10 Essential Practices | CyCognito, accessed September 13, 2025, [https://www.cycognito.com/learn/api-security/rest-api-security.php](https://www.cycognito.com/learn/api-security/rest-api-security.php)