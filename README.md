# 🌉 new-repoo — جسر Actions مجاني للريبوهات الخاصة

ريبو **public** فاضي عمدًا من أي كود أو بيانات حساسة - غرضه الوحيد إنه يشغّل
GitHub Actions لريبوهات خاصة تانية (`juleb-daily-report`، `vera-repo`) من غير
استهلاك دقائق Actions المحسوبة عليها (private repos محدودة، public repos مجانية
وغير محدودة).

## 🔧 الفكرة

كل workflow هنا بيعمل `actions/checkout` **لريبو تاني** (`repository:` +
`token:`) بدل الريبو الحالي، وبعدين بيشغّل نفس السكريبت اللي أصلاً كان بيشتغل
`self-hosted` في الريبو الخاص - بما إن `checkout` بيهيّئ الـgit remote بنفس
التوكن، أي `git push` جوه السكريبت بيوصل تلقائيًا للريبو الخاص الصحيح.

## 🔑 الإعداد المطلوب (مرة واحدة)

1. **توكن عبر-الريبوهات:** Personal Access Token (fine-grained) بصلاحية
   `Contents: Read and write` + `Actions: Read-only` على `juleb-daily-report`
   و`vera-repo` بس. يتحط هنا كـSecret اسمه `CROSS_REPO_TOKEN`.
2. **نفس أسرار الريبو الخاص المستخدمة في كل workflow** - لازم تتضاف هنا كمان
   (GitHub بيقرا `secrets.X` من الريبو اللي فيه ملف الـworkflow نفسه، مش الريبو
   المتفحوص). القائمة الدقيقة لكل workflow مكتوبة في تعليق أعلى ملفه، ودي القايمة
   الكاملة (نفس القيم بالظبط اللي عندك بالفعل في الريبوهين الخاصين):

   **دوم (`juleb-daily-report`):**
   `JULEB_URL`, `JULEB_DB`, `JULEB_USER`, `JULEB_PASS`,
   `TELEGRAM_TOKEN_DOOM`, `TELEGRAM_CHAT_ID_DOOM`,
   `JULEB_URL_DOOM`, `JULEB_DB_DOOM`, `JULEB_USER_DOOM`, `JULEB_PASS_DOOM`,
   `GROQ_API_KEY`, `GEMINI_API_KEY`, `GEMINI_API_KEY2` (اختياري),
   `TELEGRAM_CHAT_ID_STAFF` (اختياري),
   `JAHEZ_TOKEN`/`JAHEZ_STORE_ID`/`JAHEZ_WRITE_ENABLED` (اختياري).

   **فيرا (`vera-repo`):**
   `VERA_URL`, `VERA_DB`, `VERA_USER`, `VERA_PASS`,
   `VERA1_CHAT_ID`, `VERA2_CHAT_ID`, `VERA_FRIEND_CHAT_ID`.

   **مشترك بين الاتنين (نفس القيمة، ضيفه مرة واحدة بس):**
   `TELEGRAM_TOKEN`, `TELEGRAM_CHAT_ID`.

3. بعد ما `CROSS_REPO_TOKEN` والأسرار فوق تتضاف، كل الـ17 workflow هنا (9 دوم +
   8 فيرا) هتبدأ تشتغل تلقائيًا على جدولتها العادية - مفيش خطوة تالتة.

## ⚠️ ملاحظة أمان

الريبو ده لازم يفضل فاضي من أي كود/بيانات حقيقية دايمًا - أي منطق فعلي أو بيانات
حساسة مكانها الريبو الخاص فقط. لو محتاج تضيف workflow جديد، انسخ النمط اللي
موجودين واعمل checkout للريبو الخاص، متكتبش أي كود عمل هنا مباشرة.
