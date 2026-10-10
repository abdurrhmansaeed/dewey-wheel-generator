# Contributing / المساهمة

Thank you for helping improve the project! / شكرًا لمساهمتك في تحسين المشروع.

## Translations / الترجمات

1. Copy `lang/en.json` to `lang/<code>.json`. / انسخ `lang/en.json` إلى `lang/<code>.json`.
2. Translate every value under `ui`, plus `name`, `center_text` and `default_data`. Do **not** rename the keys. / ترجم كل القيم في `ui` مع `name` و`center_text` و`default_data`، ولا تغيّر أسماء المفاتيح.
3. Set `dir` (`rtl`/`ltr`), `digits`, `fonts` and `fonts_url`. Leave `is_default` as `false`. / اضبط `dir` و`digits` و`fonts` و`fonts_url`، وأبقِ `is_default` بقيمة `false`.
4. Add the file name to `lang/index.json`. / أضف اسم الملف إلى `lang/index.json`.
5. Serve the project over HTTP, generate a wheel, and check that titles fit; tune `metrics` if not. / شغّل المشروع عبر HTTP وأنشئ دائرة وتأكد أن العناوين تتسع، وعدّل `metrics` عند الحاجة.
6. Validate the JSON (e.g. `python -m json.tool lang/<code>.json`) and open a pull request. / تحقق من صحة JSON ثم افتح طلب دمج (Pull Request).

## Code changes / تعديلات الكود

The app is intentionally a single `index.html` with no build step. Keep it dependency-light and keep all user-visible text in the language files, never hard-coded in the HTML or JS.

التطبيق ملف `index.html` واحد عمدًا بلا أدوات بناء. حافظ على قلة الاعتماديات، وأبقِ كل نص ظاهر للمستخدم في ملفات اللغة وليس داخل الكود.

## Credits / الإعداد

Idea and programming: Abdurrhman Alsaeed (عبد الرحمن بن ناصر السعيد), with the assistance of Claude (Anthropic).
