# أرشيف الـ workflows (12 سبتمبر 2026)

الملفات هنا **مش محذوفة نهائيًا** - نُقلت من `.github/workflows/` لمجرد إن GitHub
Actions بس بيقرأ من `.github/workflows/` مباشرة، فوجودها هنا يوقف تسجيلها
كـ workflow نشط (يقلل الضغط على GitHub Actions scheduler) من غير ما نفقد أي كود
أو تاريخ.

**السبب:** حوالي 90 workflow اتراكموا من تشخيصات/اختبارات/إصلاحات one-off
(probes، introspection، bulk-fix بتاريخ محدد زي 9sep/10sep، أصناف SKU
0000006663 المحذوفة نهائيًا، مشروع سحب الصور المكتمل) - كل واحد منها موثّق
كمكتمل/محسوم في `PROJECT_CONTEXT.md` بريبو `juleb-daily-report`. الحجم الكبير
(128 workflow) كان أرجح سبب لملاحظة إن workflows جديدة (زي watchdog التأخير
ومزامنة الفرع التجريبي) بالكاد بتشتغل جدولتها.

**للاسترجاع:** `git mv .github/workflows_archive/<file>.yml .github/workflows/<file>.yml`
ثم commit + push - يرجع نشط فورًا بنفس التاريخ الكامل.

**قايمة كاملة بأسباب أرشفة كل ملف:** راجع رسالة الـ commit اللي نقلهم، أو
قسم "🗄️ 12 سبتمبر 2026: أرشفة ~90 workflow متراكم" في `PROJECT_CONTEXT.md`.
