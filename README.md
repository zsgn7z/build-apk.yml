# تطور المعارك — بناء ملف APK

## مهم قبل الرفع
- ملفات `package.json` و`capacitor.config.json` ومجلد `www` يجب أن تكون في **جذر** المستودع مباشرة، لا داخل مجلد فرعي.
- المجلد المخفي `.github` غالبًا لا يُرفع بالسحب والإفلات. الحل: أنشئ الملف يدويًا: Add file → Create new file، اكتب الاسم `.github/workflows/build-apk.yml` والصق محتوى `build-apk.yml` المرفق.

## الطريقة 1: من الهاتف أو الكمبيوتر بدون تثبيت شيء (GitHub)
1. أنشئ حسابًا مجانيًا على github.com وأنشئ مستودعًا جديدًا (New repository).
2. ارفع كل محتويات هذا المجلد كما هي، مع المجلد المخفي `.github` (من الكمبيوتر: Add file → Upload files).
3. افتح تبويب Actions، ثم اختر Build APK، ثم Run workflow.
4. بعد 5–10 دقائق افتح التشغيل المنتهي ونزّل الملف `battle-evolution-apk` من قسم Artifacts. بداخله `app-debug.apk`.
5. انقله إلى الهاتف وثبّته (فعّل «التثبيت من مصادر غير معروفة»).

## الطريقة 2: على جهازك
المتطلبات: Node.js 20 وJDK 17 وAndroid Studio (لتنزيل Android SDK).
```
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```
الملف الناتج: `android/app/build/outputs/apk/debug/app-debug.apk`

لقفل الوضع الأفقي، أضف `android:screenOrientation="sensorLandscape"` إلى وسم `<activity` في `android/app/src/main/AndroidManifest.xml`.

ملاحظة: هذا APK تجريبي (debug) للتثبيت المباشر. للنشر على Google Play تحتاج نسخة موقّعة (release).
