
#  مشروع بناء مسار بيانات متكامل (E-Commerce Data Pipeline) باستخدام Azure Data Factory
## وصف المشروع
يهدف هذا المشروع إلى بناء مسار بيانات (Data Pipeline) متكامل لسحب بيانات متجر إلكتروني من مصادر محلية (On-Premise) ومعالجتها على سحابة Azure. يركز المشروع على تطبيق أفضل ممارسات هندسة البيانات في عمليات الـ ETL، مع التعامل مع تحديات جودة البيانات وتوافرها.
## 🛠️ التقنيات المستخدمة (Tech Stack)
 * **Azure Data Factory (ADF):** الأداة الأساسية لإدارة وتنظيم مسارات البيانات.
 * **Mapping Data Flows:** لتنفيذ عمليات تحويل البيانات (Data Transformations) دون الحاجة لكتابة كود معقد.
 * **Self-Hosted Integration Runtime (SHIR):** للربط الآمن بين الجهاز المحلي (Local Server) وسحابة Azure.
 * **GitHub:** لإدارة النسخ وتطبيق مبادئ الـ CI/CD.
##  هندسة المسار (Pipeline Architecture)
### 1. سحب البيانات (Data Ingestion)
 * تم إعداد **Self-Hosted IR** للوصول إلى ملفات البيانات الخام (CSV) الموجودة محلياً.
 * تم استخدام **Linked Services** لتعريف المسارات والتأكد من أمان الاتصال.
### 2. معالجة وتحويل البيانات (Data Transformation)
تم استخدام **Mapping Data Flow** لتنفيذ المنطق التالي:
 * **تغيير الأسماء (Select):** إعادة تسمية الأعمدة لتناسب معايير مستودع البيانات.
 * **معالجة القيم الفارغة (Handling NULLs):** استخدام عمود مشتق (Derived Column) لمعالجة التواريخ.
 * **حل هندسي مبتكر:** لتوليد تواريخ انتهاء عشوائية فريدة لكل سجل (لأغراض محاكاة SCD Type 2)، تم استخدام المعادلة التالية:
   addDays(toDate('2025-01-01'), toInteger(abs(crc32(uuid())) % 1460))
### 3. حفظ البيانات (Data Sink)
 * تحويل البيانات المعالجة وحفظها بتنسيق **Parquet** (أو التنسيق الذي اخترته) لضمان سرعة الاستعلامات لاحقاً.
##  معرض الصور (Screenshots)
### واجهة مسار البيانات (Pipeline Overview)
توضح الرسم الهيكلي لتدفق البيانات من المصدر إلى الوجهة.
<img width="1920" height="1080" alt="Screenshot (316)" src="https://github.com/user-attachments/assets/be59bff8-5d37-4c41-a873-56d985c8045d" />


### منطق التحويل (Transformation Logic)
صورة توضح استخدام الـ Derived Column والمعادلات المتقدمة التي تم بناؤها.
<img width="1920" height="1080" alt="Screenshot (313)" src="https://github.com/user-attachments/assets/6c46d3e6-6da9-4c65-8029-36d2b14c8e25" />
<img width="1920" height="1080" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/6582cd3e-a029-47e7-986d-95c3652d7493" />


### نجاح التشغيل (Execution Success)
إثبات تشغيل الـ Pipeline بنجاح (Status: Succeeded).
<img width="1920" height="1080" alt="Screenshot (315)" src="https://github.com/user-attachments/assets/1f5b1e1a-a653-411a-9784-12271e0dbd44" />

 1
