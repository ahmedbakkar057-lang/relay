# Railway deployment

هذه النسخة مخصصة لتشغيل MS HOST على Railway كخدمة Node.js دائمة، بما في ذلك تشغيل بوتات المستخدمين.

## النشر

1. ارفع المشروع إلى GitHub أو ارفع ملف ZIP في Railway.
2. أنشئ **New Project → Deploy from GitHub Repo**.
3. Railway سيكتشف Node.js ويستخدم `npm ci --omit=dev` ثم `npm start`. يوجد أيضًا `railway.json` و`Procfile` جاهزان.
4. أضف متغيرات البيئة التالية في Variables:

```env
ADMIN_EMAIL=wemohammed1@gmail.com
ADMIN_PASSWORD=bakkar12
PUBLIC_REGISTRATION=true
NODE_ENV=production
```

Railway يمرر `PORT` تلقائيًا، والخادم يستمع عليه. لا تضع رقم منفذ ثابت.

## التخزين الدائم

الملفات وقاعدة البيانات تحفظ داخل `db.json` و`USERS/`. أضف **Railway Volume** واربطه على `/app` (أو اضبط `DB_FILE` و`USERS_DIR` إلى مسار داخل Volume) حتى لا تضيع الحسابات والبوتات بعد إعادة النشر أو إعادة إنشاء الخدمة.

## ملاحظات البوتات

Railway مناسب للعمليات الدائمة، لكن يجب أن تكون الخطة/الخدمة قادرة على تشغيل عمليات Node.js فرعية. كل بوت يحصل على `PORT` داخلي مخصص؛ إذا كان البوت يحتاج اتصالًا خارجيًا مباشرًا، استخدم WebSocket/HTTP عبر الخادم أو إعداد شبكة مناسب، لأن المنافذ العامة الإضافية ليست مضمونة تلقائيًا.
