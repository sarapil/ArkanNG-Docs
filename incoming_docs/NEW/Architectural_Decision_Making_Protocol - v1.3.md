

## **بروتوكول اتخاذ القرارات المعمارية (Architectural\_Decision\_Making\_Protocol) \- v1.3**

### **10.1: تفويض وعملية سجل القرارات المعمارية (ADR)**

* **التفويض:** يجب إنشاء سجل قرار معماري (ADR) لكل قرار مهم معماريًا.\[36, 37\]  
* **العملية:**  
  1. **تحديد الحاجة:** يمكن لأي عضو في الفريق تحديد الحاجة إلى قرار معماري.  
  2. **صياغة ADR:** يتم تعيين مالك لصياغة ADR باستخدام قالبنا القياسي. الحالة الأولية هي "مقترح".\[36\]  
  3. **المراجعة:** يتم تقديم ADR للمراجعة من قبل أعضاء الفريق المعنيين.  
  4. **القرار:** تكون نتيجة المراجعة تغييرًا في حالة ADR إلى "مقبول" أو "مرفوض" أو "تم استبداله".\[36\]  
  5. **سجل غير قابل للتغيير:** بمجرد اتخاذ القرار، يصبح ADR سجلاً غير قابل للتغيير.\[36\]

### **10.2: قالب ADR القياسي (مبني على MADR)**

سنعتمد تنسيق سجلات القرارات المعمارية بـ Markdown (MADR) لهيكله الخفيف والملائم للمطورين.\[37\]

---

LOG\_DECISION  
Title: ADR-0001: Adoption of MADR for Documenting Architectural Decisions  
Status: Accepted  
Date: 2025-06-15  
Context and Problem Statement: As the company grows, verbal or ad-hoc decisions about our software architecture will become a significant liability. New team members will lack context, past decisions may be re-litigated, and the rationale behind our system's design will be lost. We need a lightweight, consistent, and developer-friendly process for documenting significant architectural choices.  
Decision Drivers:

* Need for a "Single Source of Truth" for architectural rationale.  
* Requirement to accelerate onboarding for new engineers.  
* Desire to avoid "analysis paralysis" with a lean documentation format.  
* Alignment with our "Documentation as Code" and "Transparent by Default" core values.  
  Considered Options:  
1. **MADR (Markdown Architectural Decision Records):** A lightweight template using Markdown, stored in Git.  
2. **Michael Nygard's ADR Template:** The original, more verbose template.  
3. Wiki-based Documentation (e.g., Confluence): Using a dedicated wiki page for each decision.  
   Decision Outcome:  
   Chosen option: "MADR (Markdown Architectural Decision Records)", because it perfectly aligns with our core principles. Its Markdown format makes it easy for developers to write and review within their existing tools (IDE, Git). Storing ADRs in our code repository treats them as version-controlled artifacts, fulfilling the "Documentation as Code" principle. Its lean structure \[37\] prevents unnecessary bureaucracy while capturing all essential information: context, options, decision, and consequences.\[37\]  
   Consequences:  
* **Good:** Establishes a clear, scalable process for technical governance from day one. Creates a valuable, searchable decision log that will become a strategic asset for team growth.  
* **Bad:** Requires discipline from the engineering team to consistently create and maintain ADRs for all significant decisions. This initial effort represents an overhead compared to making no documentation.

---

LOG\_DECISION  
Title: ADR-0002: Adoption of a Modular Application Ecosystem over a Monolithic ERP Approach  
Status: Accepted  
Date: 2025-09-12  
Context and Problem Statement: The initial project plan was centered around customizing a monolithic ERP application. While comprehensive, this approach presents challenges in delivering a best-in-class user experience for each specific business function (HR, CRM, Support). Monolithic systems often result in modules that are functional but not exceptional, with a UI/UX that can feel dated and less intuitive compared to specialized SaaS products. This limits our ability to compete effectively in individual market segments and can hinder user adoption.  
Decision Drivers:

* The need for a superior, modern, and focused user experience for each business domain (Sales, HR, Support, etc.).  
* The strategic direction of Frappe Technologies itself, which is moving towards a suite of independent, high-performance applications built with modern frontend frameworks like Vue.js.\[1\]  
* The requirement for greater business model flexibility, allowing us to offer standalone solutions (e.g., just a CRM) in addition to the fully integrated **ArkanNG** suite.  
* The need to accelerate development and innovation cycles for each business function independently, without the risks associated with modifying a large, monolithic codebase.\[38\]  
  Considered Options:  
1. **Continue with the Monolithic Model:** Customize the existing modules within a single ERP to meet all requirements.  
2. **Adopt a Hybrid Model:** Use a core ERP for some functions and integrate with third-party SaaS applications for others (e.g., Salesforce for CRM, Zendesk for Support).  
3. Adopt the Modern Frappe Application Ecosystem: Build our core ArkanNG offering around the suite of modern, independent Frappe applications (Frappe HR, Frappe CRM, Frappe Helpdesk, Frappe Books, etc.), ensuring they are tightly integrated.  
   Decision Outcome:  
   Chosen option: "Adopt the Modern Frappe Application Ecosystem". This decision aligns our architecture with the future of the Frappe framework. By adopting specialized applications like Frappe HR, Frappe CRM, and Frappe Helpdesk, we gain a significant competitive advantage through superior UI/UX and focused functionality.\[1, 39\] While these apps are independent, their shared foundation on the Frappe Framework and a unified database allows for deep integration. Frappe Insights will serve as the strategic tool to unify data across these applications, mitigating the risk of data silos and providing the 360-degree view promised by traditional ERPs.\[40, 41\] This modular approach provides the best of both worlds: specialized excellence and integrated power.  
   Consequences:  
* **Good:** We can now compete directly with best-of-breed SaaS solutions in each vertical (CRM, HR, etc.). Our go-to-market strategy becomes significantly more flexible. User adoption rates are expected to be higher due to a better user experience.  
* **Bad:** The operational complexity of managing multiple distinct applications increases. We must invest in ensuring seamless data flow and a consistent user experience between applications. This places a greater strategic importance on the role of **Frappe Insights** as our central data intelligence layer.

---

LOG\_DECISION  
Title: ADR-0003: Formal Adoption of the Curated Frappe Application Suite  
Status: Accepted  
Date: 2025-09-15  
Context and Problem Statement: Following the strategic decision to adopt a modular architecture (ADR-0002), a comprehensive analysis of available official and community applications was conducted. To move from strategy to execution, a formal decision is required to define the specific set of applications that will form the core of the ArkanNG platform. This decision aims to prevent architectural drift, ensure alignment across development teams, and leverage mature, well-supported applications to accelerate development.  
Decision Drivers:

* Need to accelerate time-to-market by using pre-built, high-quality applications.  
* Desire to align with the official Frappe technology stack to ensure long-term support and compatibility.  
* Requirement for specific functionalities (VoIP, real-time chat, knowledge management, biometric attendance) that are critical to our business model.  
* Need for guaranteed legal and fiscal compliance in target markets (KSA, UAE).  
  Considered Options:  
1. **Develop all functionalities in-house:** Build every required module from scratch as custom Frappe apps.  
2. **Rely heavily on third-party community apps:** Integrate a wide range of community-developed apps for core functionalities.  
3. Adopt a curated suite of official and select community apps: Formally adopt a specific list of high-quality, mostly official Frappe applications as the standard foundation for ArkanNG, and build custom logic on top of them.  
   Decision Outcome:  
   Chosen option: "Adopt a curated suite of official and select community apps". This approach provides the optimal balance between speed, quality, and strategic control. We will formally adopt the following applications as part of the core ArkanNG stack: frappe/payments, frappe/telephony, frappe/wiki, frappe/chat, frappe/meeting, frappe/KSA, frappe/erpnext\_uae, and frappe/biometric-attendance-sync-tool. We will also adopt yrestom/erpnext\_telegram after a security review. This decision allows us to inherit mature functionality while focusing our custom development efforts on our unique value propositions, such as the localized AI engine and digital agents.  
   Consequences:  
* **Good:** Development roadmap is significantly accelerated. We inherit robust, community-tested solutions for complex domains like telephony and local compliance. Our internal teams can focus on high-value, differentiating features.  
* **Bad:** We introduce a dependency on the release cycles and maintenance of these external applications. For the selected community app (erpnext\_telegram), we must allocate resources for ongoing security reviews and potential maintenance. The overall operational complexity of the platform increases.