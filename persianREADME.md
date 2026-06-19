# 🔑 Open AG Patcher (ترجمه فارسی راهنما)

پچر متن‌باز (Open Source) برای Antigravity IDE و اپلیکیشن standalone آن: محدودیت‌های منطقه‌ای را بدون نیاز به VPN و بدون تغییر منطقه‌ی حساب گوگل برمی‌دارد. این ابزار، نسخه‌ی متن‌باز معادل ابزار «Antigravity IDE در روسیه بدون VPN و بدون تغییر منطقه حساب گوگل» است.

## 🎦 ویدیو راهنمای نصب و رفع مشکلات
لینک‌های ویدیو در یوتیوب، Dzen، VK Video و تلگرام در فایل اصلی موجود است (لینک‌ها دست‌نخورده باقی مانده‌اند).

## ⚠️ خطای HTTP 500 Internal Server Error
اگر هنگام درخواست در Antigravity IDE خطای HTTP 500 Internal Server Error ظاهر شد، کاری نمی‌توان کرد؛ باید حساب کاربری را عوض کنید (ترجیحاً به منطقه‌ای که Antigravity IDE رسماً در آن کار می‌کند یا اشتراک پولی خریداری شده). حتی ابزارهای پولی هم این مشکل را حل نمی‌کنند.

(نمونه‌ی خروجی خطا در فایل اصلی، بدون تغییر باقی می‌ماند.)

## ⚠️ خطای HTTP 429 Too Many Requests
اگر با خطای `HTTP 429 Too Many Requests` مواجه شدید، یعنی محدودیت (کوتای) سمت گوگل تمام شده است. معمولاً این مشکل به دلیل اتصال نشست (session) به کوتای تمام‌شده رخ می‌دهد.

**راه‌حل:**
1. از قابلیت داخلی پچر استفاده کنید — **گزینه‌ی ۷: Fix HTTP 429 (Too Many Requests)**.
   - این اسکریپت از پوشه‌ی داده‌ها بکاپ می‌گیرد، تنظیمات قدیمی را پاک می‌کند (توکن‌ها/کوتا را ریست می‌کند)، اما **گفتگوهای شما حفظ می‌شوند**.
   - بعد از اجرا باید دوباره وارد حساب کاربری شوید.
2. اگر فیکس داخلی کمکی نکرد — حساب گوگل خود را عوض کنید.
3. **مهم:** استفاده از VPN یا روش‌های دیگر دور زدن محدودیت‌ها ممکن است توسط گوگل شناسایی شود و باعث بازگشت خطای 429 شود.

جزئیات بیشتر در [issue #10](https://github.com/AvenCores/open-antigravity-patcher/issues/10).

## ⚠️ خطای HTTP 400 Bad Request
اگر خطای `HTTP 400 Bad Request` با پیام `User location is not supported for the API use` دریافت کردید، یعنی گوگل موقعیت مکانی شما را پشتیبانی‌نشده تشخیص داده است.

**مهم:** استفاده از VPN، پراکسی یا سایر روش‌های دور زدن محدودیت ممکن است توسط گوگل شناسایی شده و منجر به همین خطا شود. گوگل فعالانه با روش‌های دور زدن مبارزه می‌کند و اگر آی‌پی یا سایر پارامترهای نشست شما مشکوک به نظر برسد، دسترسی ممکن است مسدود شود.

**راه‌حل:**
1. اگر از Antigravity IDE نسخه‌ی **1.23.0 یا بالاتر** استفاده می‌کنید، پچ را اعمال کنید (**گزینه‌ی ۱: Apply patch**). پچر به‌طور خودکار پارامترهای لازم را برای دور زدن این خطا به `settings.json` اضافه می‌کند (جزئیات بیشتر در بخش «راه‌حل موقت runtime settings» در ادامه).
2. اگر پچ از قبل اعمال شده یا نسخه پایین‌تر از 1.23 است، سعی کنید حساب گوگل را عوض کنید یا از VPN دیگری استفاده کنید.
3. می‌توانید از **[Xbox DNS](https://xbox-dns.ru/)** استفاده کنید (سرورهای DNS مخصوص برای دور زدن محدودیت‌ها روی کامپیوتر یا روتر).

## 📚 اطلاعات تکمیلی درباره خطاها
برای درک عمیق‌تر انواع خطاهای HTTP و روش‌های عیب‌یابی آن‌ها، مطالعه این راهنما توصیه می‌شود:
- [5xx Server Errors: The Complete Guide](https://komodor.com/learn/5xx-server-errors-the-complete-guide/) — بررسی کامل خطاهای سمت سرور.

## 🌟 امکانات
- جست‌وجوی خودکار نصب Antigravity IDE، اپلیکیشن standalone آن و Antigravity CLI (`agy`) در مسیرهای استاندارد و رجیستری ویندوز.
- **پچ Antigravity CLI** — حذف صفحه‌ی «Eligibility Check» در باینری Go (`agy`/`agy.exe`) در سطح کد ماشین، بر اساس امضای بایتی (همراه با بکاپ و امکان بازگردانی).
- باز کردن، تغییر و بسته‌بندی مجدد کامل `app.asar` برای Antigravity با حفظ ساختار فایل‌های خارجیِ از حالت فشرده خارج‌شده (`.unpacked`).
- سرور پراکسی HTTP محلی یکپارچه برای پچ پویا (dynamic) کد جاوااسکریپتِ بارگذاری‌شده در اپلیکیشن standalone.
- پشتیبانی از لینوکس: جست‌وجو در `/usr/share/antigravity-ide`، تشخیص نسخه از طریق `dpkg`، `rpm` و `package.json`.
- پشتیبانی از macOS: جست‌وجوی بسته‌ی `.app` در `/Applications` و `~/Applications`، امضای مجدد ad-hoc پس از تغییر `main.js` یا `app.asar`.
- ایجاد بکاپ پیش از هرگونه تغییر.
- اعمال و بازگردانی پچ از طریق منوی ساده.
- پشتیبانی از مسیرهای `resources/app/out/main.js` و `resources/app/main.js`.
- خروجی رنگی و تلاش خودکار برای ارتقای سطح دسترسی (UAC در ویندوز، پیشنهاد `sudo` در لینوکس).
- بررسی حداقل نسخه‌ی Antigravity IDE (>= `2.0.1`) پیش از اعمال پچ.
- تشخیص نسخه‌ی Antigravity IDE از طریق رجیستری ویندوز، پکیج‌منیجر لینوکس یا `package.json` در macOS.
- شناسایی پچ از قبل اعمال‌شده با پیشنهاد اعمال مجدد.
- راه‌حل موقت runtime برای Antigravity IDE نسخه‌ی `1.23+`: ثابت کردن endpoint پایدار Cloud Code و غیرفعال‌کردن آزمایش‌های مشکل‌دار Cascade/model از طریق `settings.json`.

## 🚀 روش استفاده
1. Antigravity IDE یا Antigravity را ببندید.
2. پچر را با دسترسی ادمین اجرا کنید (اسکریپت خودش در صورت نیاز درخواست ارتقای دسترسی می‌دهد).
3. در منو، گزینه‌ی مورد نظر را انتخاب کنید:

| گزینه‌ی منو | توضیح |
|---|---|
| `1. Apply Antigravity IDE patch` | اعمال پچ روی `main.js` برای Antigravity IDE |
| `2. Apply Antigravity patch` | اعمال پچ روی `app.asar` برای نسخه‌ی standalone |
| `3. Apply Antigravity CLI (agy) patch` | اعمال پچ روی باینری `agy`/`agy.exe` برای Antigravity CLI |
| `4. Restore Antigravity IDE from backup` | بازگردانی `main.js` اصلی برای Antigravity IDE |
| `5. Restore Antigravity from backup` | بازگردانی `app.asar` اصلی برای نسخه‌ی standalone |
| `6. Restore Antigravity CLI from backup` | بازگردانی `agy`/`agy.exe` اصلی |
| `7. Fix HTTP 429` | ریست تنظیمات برای رفع خطای 429 (گفتگوها حفظ می‌شوند) |
| `8. Open GitHub repository` | باز کردن صفحه‌ی پروژه در مرورگر |
| `9. Select custom path` | انتخاب دستی مسیر پوشه یا فایل اپلیکیشن |
| `0. Exit` | خروج |

اجرا از سورس:
```bash
python main.py
```

اجرا با مشخص‌کردن مسیر (برای Antigravity IDE، Antigravity standalone یا Antigravity CLI):
```bash
# ویندوز
python main.py "C:\Users\<username>\AppData\Local\Programs\Antigravity IDE"
python main.py "C:\Users\<username>\AppData\Local\Programs\Antigravity\resources\app.asar"
python main.py "C:\Users\<username>\AppData\Local\agy\bin\agy.exe"

# لینوکس
python main.py /usr/share/antigravity-ide
python main.py /opt/Antigravity
python main.py /usr/local/bin/agy

# macOS
python3 main.py /Applications/Antigravity\ IDE.app
python3 main.py /Applications/Antigravity.app
python3 main.py /usr/local/bin/agy
```

اگر `main.js` یا `app.asar` کنار اسکریپت قرار داشته باشد، نیازی به مشخص‌کردن مسیر نیست — به‌طور خودکار پیدا می‌شوند.

> **macOS:** اگر `Antigravity IDE.app` در `/Applications` باشد، نوشتن نیاز به `sudo` دارد (اسکریپت خودش پیشنهاد اجرای مجدد می‌دهد). برای نصب در `~/Applications` یا پوشه‌ی شخصی، `sudo` لازم نیست. پس از پچ موفق، `.app` به‌طور خودکار با امضای ad-hoc دوباره امضا می‌شود (`codesign --force --deep --sign -`) — بدون این کار، Electron با Hardened Runtime روی macOS اجرا نخواهد شد.

### 🍎 استفاده در macOS
از آنجا که نسخه‌های آماده‌ی باینری برای macOS در ریلیزهای رسمی موجود نیستند (فقط برای ویندوز و لینوکس در دسترس‌اند)، می‌توانید پچر را مستقیماً از سورس اجرا کنید یا خودتان فایل اجرایی بسازید.

**روش ۱: اجرا از سورس (توصیه‌شده)**
1. محیط مجازی بسازید، فعالش کنید و وابستگی‌های لازم را نصب کنید:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
2. Antigravity یا Antigravity IDE را کاملاً ببندید.
3. پچر را با مشخص‌کردن مسیر اپلیکیشن اجرا کنید:
   ```bash
   # برای Antigravity IDE
   python3 main.py "/Applications/Antigravity IDE.app"
   
   # برای نسخه‌ی standalone
   python3 main.py "/Applications/Antigravity.app"
   ```
   *نکته: اگر اپلیکیشن در پوشه‌ی `/Applications` باشد، اسکریپت به‌طور خودکار درخواست ارتقای دسترسی (`sudo`) برای نوشتن می‌دهد.*

**روش ۲: ساخت دستی فایل باینری**
اگر به فایل اجرایی آماده نیاز دارید، می‌توانید طبق دستورالعمل بخش «🛠️ Build» خودتان آن را بسازید.

پس از ساخت موفق، اجرای فایل کامپایل‌شده از طریق Terminal:
```bash
cd dist
chmod +x Open_AG_Patcher_macOS
sudo ./Open_AG_Patcher_macOS
```
اگر macOS اجرای فایل کامپایل‌شده را مسدود کرد، ویژگی quarantine را بردارید:
```bash
xattr -dr com.apple.quarantine Open_AG_Patcher_macOS
```

**چه گزینه‌ای در منو انتخاب کنیم:**
- `1. Apply Antigravity IDE patch` برای `Antigravity IDE.app`
- `2. Apply Antigravity patch` برای `Antigravity.app` (standalone)
- `3. Apply Antigravity CLI (agy) patch` برای باینری `agy` (در صورت نصب)
- `4`، `5` یا `6` برای بازگردانی از بکاپ

برای `Antigravity.app` نسخه‌ی standalone، پچر معمولاً خودش پیدا می‌کند:
```text
/Applications/Antigravity.app
```
اگر جست‌وجوی خودکار اپلیکیشن را پیدا نکرد، گزینه‌ی `9. Select custom path` را انتخاب و یکی از مسیرهای زیر را وارد کنید:
```text
/Applications/Antigravity.app
/Applications/Antigravity IDE.app
```

**بررسی امضا:**
بعد از پچ، `.app` به‌طور خودکار با امضای ad-hoc دوباره امضا می‌شود. برای بررسی:
```bash
codesign -dv /Applications/Antigravity.app 2>&1 | grep Signature
```
خروجی مورد انتظار:
```text
Signature=adhoc
```

## ❓ دقیقاً چه چیزی تغییر می‌کند

### پچ برای Antigravity IDE
پچر **۴ تغییر** در `main.js` اعمال می‌کند و علاوه بر آن یک راه‌حل موقت runtime جداگانه در `settings.json` کاربر اعمال می‌کند. تغییرات `main.js` از طریق بکاپ (`main.js.bak`) قابل بازگشت است، و `settings.json` نیز پیش از نوشتن، در یک بکاپ جداگانه ذخیره می‌شود.

**۱. `if(isGoogleInternal)` → `if(true)`**
بررسی فلگ `isGoogleInternal` را به‌صورت بدون‌قید‌و‌شرط `true` تغییر می‌دهد و محدودیت‌های منطقه‌ای/داخلی را برمی‌دارد. این تغییر روی همه‌ی مواردِ مشابه در فایل اعمال می‌شود (الگوی `if(this.<svc>.isGoogleInternal)`).

**۲. `if(X(),this.Y.isGoogleInternal)` → `if(X(),true)` (سرویس احراز هویت)**
سرویس auth بسته به نسخه، الگوهای متفاوتی را بررسی می‌کند:
- **نسخه‌ی 1.22–1.22.x:** `if(this.w.resetIsTierGCPTos(),this.t.isGoogleInternal)` → `if(this.w.resetIsTierGCPTos(),true)`
- **نسخه‌ی 1.23+:** `if(this.t.send({...}),this.y.resetIsTierGCPTos(),this.w.isGoogleInternal)` → `if(this.t.send({...}),this.y.resetIsTierGCPTos(),true)`

پچر به‌طور خودکار نسخه‌ی Antigravity IDE را تشخیص می‌دهد و الگوی متناسب با آن را اعمال می‌کند.

**۳. `ideName` → `"antigravity-insiders"`**
مقدار `ideName:"antigravity"` را به `ideName:"antigravity-insiders"` تغییر می‌دهد تا شناسایی کلاینت به‌درستی انجام شود.

**۴. صفحه‌ی `ineligible` — دور زدن (نسخه‌ی 1.22+)**
عبارت ternary `...s?{}:{errorType:"ineligible",reason:a,verificationUrl:i}` را به `...s?{}:{}` تغییر می‌دهد — خطای ineligible دیگر ارسال نمی‌شود و صفحه‌ی مسدودسازی نمایش داده نمی‌شود.

**۵. راه‌حل موقت runtime settings (نسخه‌ی 1.23+)**
از نسخه‌ی Antigravity IDE `1.23+` به بعد، بخشی از کاربران پس از آپدیت با این خطا مواجه می‌شوند:
```json
{
  "error": {
    "code": 400,
    "message": "User location is not supported for the API use.",
    "status": "FAILED_PRECONDITION"
  }
}
```
در لاگ‌ها در این حالت درخواست‌هایی به `daily-cloudcode-pa.googleapis.com` و آزمایش‌های جدید Cascade/model دیده می‌شوند. این یک راه‌حل موقت است؛ بهتر است وقتی Antigravity IDE مسیر/آزمایش جدید را پایدار کرد یا رفتار سازگار را بازگرداند، این تنظیم حذف یا بازبینی شود. این راه‌حل موقت، موارد زیر را به `settings.json` کاربر اضافه می‌کند:
```json
{
  "jetski.cloudCodeUrl": "https://cloudcode-pa.googleapis.com",
  "codeiumDev.forceDisableExperiments": "CASCADE_DEFAULT_MODEL_OVERRIDE,CASCADE_USE_EXPERIMENT_CHECKPOINTER,CASCADE_NEW_MODELS_NUX,CASCADE_NEW_WAVE_2_MODELS_NUX",
  "codeiumDev.languageServerEnv": {
    "BORG_DISABLE_EXPERIMENTS": "CASCADE_DEFAULT_MODEL_OVERRIDE,CASCADE_USE_EXPERIMENT_CHECKPOINTER,CASCADE_NEW_MODELS_NUX,CASCADE_NEW_WAVE_2_MODELS_NUX",
    "BORG_EXPERIMENTS": ""
  }
}
```
اگر `settings.json` از قبل وجود داشته باشد، پیش از تغییر، یک بکاپ به‌شکل `settings.json.bak-YYYYMMDD-HHMMSS` ساخته می‌شود. اگر `main.js` از قبل پچ شده باشد، گزینه‌ی `Apply patch` همچنان راه‌حل موقت runtime را بدون نیاز به تغییر مجدد `main.js` اعمال می‌کند.

### پچ برای Antigravity Standalone (ASAR)
برای نسخه‌ی standalone، فرایند پچ متفاوت است چون منطق رابط کاربری به‌صورت پویا از شبکه بارگذاری می‌شود:
1. آرشیو اصلی در یک بکاپ با نام `app.asar.bak` (یا `app1.asar.bak`) کپی می‌شود تا امکان بازگشت بعدی وجود داشته باشد، و خود آرشیو در یک پوشه‌ی موقت از حالت فشرده خارج می‌شود.
2. در فایل `dist/main.js` یک رهگیر (interceptor) درخواست‌های شبکه ثبت می‌شود.
3. هنگام اجرای Antigravity، تمام درخواست‌ها به اسکریپت‌های فرانت‌اند (`/main.js`) به سمت یک سرور پراکسی HTTP محلی که داخل خود اپلیکیشن ساخته می‌شود، هدایت می‌شوند.
4. سرور پراکسی، اسکریپت فرانت‌اند اصلی را دانلود می‌کند، در لحظه بررسی‌های `isGoogleInternal` را به `true` تغییر می‌دهد، وضعیت‌های خطای احراز هویت را به ورود موفق (`signedIn`) هدایت می‌کند، نتیجه را کش می‌کند و آن را به اپلیکیشن تحویل می‌دهد.
5. فایل‌های تغییریافته دوباره در `app.asar` بسته‌بندی می‌شوند، با محاسبه‌ی صحیح هش‌های یکپارچگی (بلوک‌های SHA256) و حفظ ساختار فایل‌های خارجی از حالت فشرده خارج‌شده (`.unpacked`).

> **نکته:**
> - پچ «onboardUser injection» از نسخه‌ی 1.22+ غیرفعال شده، چون در نسخه‌های جدید Antigravity IDE تابع `onboardUser` به‌طور بومی فراخوانی می‌شود و تزریق آن، فراخوانی را تکراری کرده و روند احراز هویت را خراب می‌کند.
> - از نسخه‌ی 1.0.8 پچر به بعد، **انتخاب نسخه‌محورِ الگوی auth** انجام می‌شود: برای نسخه‌های Antigravity IDE پایین‌تر از 1.23 الگوی قدیمی، و برای نسخه‌ی 1.23+ الگوی جدید با فراخوانی اضافه‌ی `send()` اعمال می‌شود.

### پچ برای Antigravity CLI (agy)
Antigravity CLI یک باینری مستقل به زبان Go است (`agy.exe` در ویندوز، `agy` در لینوکس/macOS) که آن هم یک صفحه‌ی ظاهری «Eligibility Check» نمایش می‌دهد که مانع ادامه‌ی کار می‌شود. چون این فایل کامپایل‌شده است (نه جاوااسکریپت)، پچ آن **در سطح کد ماشین** و بر اساس امضای منحصربه‌فرد بایتی انجام می‌شود.

1. در تابع `handleAuthResult`، دروازه‌ی eligibility بر اساس فیلد سمت سرور `AuthResult.hasValidAuth` (بایت در آفست `+8`) ساخته می‌شود:
   ```asm
   test rax,rax      ; 48 85 c0
   je   ...          ; 0f 84 xx xx xx xx
   cmp  byte[rax+8],0; 80 78 08 00     <-- بررسی eligibility
   jne  ...          ; 0f 85 xx xx xx xx
   ```
2. پچر این دنباله را بر اساس امضا (با wildcard برای بایت‌های displacement) پیدا می‌کند و `cmp byte[rax+8],0` را به `test rax,rax ; nop` (`48 85 c0 90`) بازنویسی می‌کند. در نتیجه `ZF=0` می‌شود و پرش شرطی `jne` همیشه مسیر «eligible» را انتخاب می‌کند — صفحه‌ی Eligibility دیگر نمایش داده نمی‌شود.
3. پیش از نوشتن، یک بکاپ با نام `agy.exe.agybak` (یا `agy.agybak` در POSIX) ساخته می‌شود. اگر بکاپ موجود قدیمی باشد (اپلیکیشن به‌طور خودکار آپدیت شده)، به‌طور خودکار به‌روزرسانی می‌شود — نسخه‌ی قدیمی نگه داشته نمی‌شود.
4. در macOS پس از تغییر، باینری دوباره با امضای ad-hoc امضا می‌شود (مشابه `.app`).

**ایمنی پچ:**
- اگر امضای بایتی در باینری پیدا نشود (نسخه‌ی ناشناخته/پشتیبانی‌نشده)، پچر **از پچ‌کردن خودداری می‌کند** و چیزی تغییر نمی‌دهد — پیام «signature not found (unsupported version?)» نمایش داده می‌شود.
- اگر امضا بیش از یک‌بار یافت شود، پچر هم باز خودداری می‌کند («not unique — refusing to guess») — حدس نمی‌زند که کدام محل را تغییر دهد.
- بازگردانی از طریق گزینه‌ی `6. Restore Antigravity CLI from backup` و بازیابی از `.agybak` انجام می‌شود.

> **نکته‌ی پلتفرمی:** این امضا روی ویندوز (باینری Go با نام `agy.exe`) تست شده است. جست‌وجوی فایل به‌صورت کراس‌پلتفرم انجام می‌شود (`PATH`، scoop در ویندوز، `/usr/local/bin`، `/opt/antigravity/bin`، `~/.local/bin` در POSIX). در لینوکس/macOS ممکن است باینری `agy` متفاوت کامپایل شده باشد و امضا مطابقت نداشته باشد — در این صورت پچر صادقانه بدون تغییر فایل، این موضوع را اعلام می‌کند.

## 🔍 منطق جست‌وجوی فایل
پچر `main.js` را به این ترتیب جست‌وجو می‌کند:
1. آرگومان خط فرمان (مسیر پوشه یا مستقیماً `main.js`).
2. پوشه‌ی فعلی (`./main.js`).
3. جست‌وجوی خودکار در مسیرهای استاندارد:
   - **ویندوز:** `%LOCALAPPDATA%\Programs\Antigravity IDE`
   - **لینوکس:** `/usr/share/antigravity-ide`، `/opt/Antigravity IDE`، `/opt/Antigravity IDE/resources/app/out`
   - **macOS:** `/Applications/Antigravity IDE.app/Contents/Resources/app`، `~/Applications/Antigravity IDE.app/Contents/Resources/app`
4. رجیستری ویندوز (کلید `{AA73B3E3-C6C8-45C8-B1DC-4AE56C751432}_is1` در `HKCU` و `HKLM`: `SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\`).

داخل پوشه‌ی یافت‌شده، مسیرهای زیر بررسی می‌شوند:
- `resources/app/out/main.js`
- `resources/app/main.js`
- `out/main.js` (macOS)
- `main.js` (در صورت مشخص‌شدن مستقیم مسیر)

در macOS، اسکریپت مسیر بسته‌ی `.app` را هم مستقیماً می‌پذیرد — `Contents/Resources/app/out/main.js` به‌طور خودکار resolve می‌شود.

### جست‌وجوی Antigravity CLI (`agy`)
باینری `agy` (`agy.exe` در ویندوز) به‌صورت مستقل از مکان (location-agnostic) جست‌وجو می‌شود — از طریق `PATH` و پوشه‌های استاندارد، بدون مسیر/نسخه‌ی هاردکد:
1. آرگومان خط فرمان یا گزینه‌ی `9. Select custom path → 3` (مسیر فایل `agy`/`agy.exe` یا پوشه).
2. `PATH` (`shutil.which("agy")`).
3. پوشه‌های استاندارد:
   - **ویندوز:** `%LOCALAPPDATA%`، `%PROGRAMFILES%`، `%PROGRAMFILES(X86)%`، `%ProgramData%`، `%APPDATA%` (+ زیرپوشه‌ی `Programs`)، scoop (`%USERPROFILE%\scoop\apps`، `%SCOOP%\apps`). الگوها: `agy/bin/agy.exe`، `agy/*/bin/agy.exe` (پوشه‌های نسخه‌ی scoop)، `agy*/agy.exe`.
   - **لینوکس/macOS:** `/usr/local/bin`، `/usr/bin`، `/opt/antigravity/bin`، `/opt/antigravity`، `~/.local/bin`، `~/bin`.

اگر چند نسخه پیدا شود (مثلاً scoop با چند نسخه)، جدیدترین بر اساس mtime انتخاب می‌شود.

## 🔎 تشخیص نسخه‌ی Antigravity IDE

| پلتفرم | روش تشخیص نسخه |
|---|---|
| **ویندوز** | رجیستری: `DisplayVersion` از کلید `{AA73B3E3-...}_is1` |
| **لینوکس (deb)** | `dpkg-query -W antigravity-ide` |
| **لینوکس (rpm)** | `rpm -q --queryformat %{VERSION} antigravity-ide` |
| **لینوکس (portable/snap/flatpak)** | `package.json` کنار `main.js` |
| **macOS** | `package.json` در `Antigravity IDE.app/Contents/Resources/app/` |

اگر نسخه تشخیص داده نشود، پچر پیشنهاد ادامه بدون بررسی را می‌دهد. اگر نسخه پایین‌تر از `1.22.2` باشد، هشدار می‌دهد و باز هم امکان انتخاب می‌دهد.

## 🔒 بررسی پچ از قبل‌اعمال‌شده
پیش از پچ‌کردن، اسکریپت بررسی می‌کند که آیا فایل از قبل پچ شده یا نه، بر اساس دو نشانه:
- نبودِ `if(this.X.isGoogleInternal)` (الگو با `if(true)` جایگزین شده)
- وجود رشته‌ی `"antigravity-insiders"`

اگر هر دو نشانه پیدا شود، هشداری همراه با درخواست تأیید برای اعمال مجدد نمایش داده می‌شود.

## 🛡️ ارتقای سطح دسترسی
- **ویندوز:** درخواست خودکار UAC از طریق `ShellExecuteW` با پارامتر `runas`. مسیرهای دارای فاصله را به‌درستی مدیریت می‌کند.
- **لینوکس:** اگر اسکریپت با کاربر root اجرا نشده باشد، پیشنهاد می‌دهد دوباره با `sudo` اجرا شود (`os.execvp`). در صورت رد، با هشدار درباره‌ی خطاهای احتمالی نوشتن، ادامه می‌دهد. در این حالت، راه‌حل موقت runtime در `settings.json` کاربر اصلی (`SUDO_USER`/`SUDO_UID`) نوشته می‌شود، نه در `/root/.config/...`.
- **macOS:** از همان مسیر posix استفاده می‌شود — اگر بدون root اجرا شده باشد، `sudo` پیشنهاد می‌شود. برای `~/Applications/Antigravity IDE.app` می‌توان به درخواست `sudo` پاسخ «خیر» داد (چون پوشه از قبل قابل نوشتن است)، اما برای `/Applications/Antigravity IDE.app` باید موافقت کرد. در اجرا با `sudo`، فایل `settings.json` کاربر هم از home کاربر اصلی خوانده می‌شود، نه از `root`.

## 🍎 نکات ویژه‌ی macOS

**امضای مجدد `.app` پس از پچ**
هرگونه تغییر در فایل داخل بسته‌ی امضاشده‌ی `.app`، امضای کد (code signature) را خراب می‌کند. اپلیکیشن‌های الکترونی با Hardened Runtime فعال (که Antigravity IDE یکی از آن‌هاست) پس از این تغییر، روی macOS **اجرا نمی‌شوند** — حتی پیش از آنکه Gatekeeper دیالوگی به کاربر نشان دهد.

برای اینکه `.app` همچنان کار کند، اسکریپت پس از `do_patch` و `do_restore` به‌طور خودکار این دستورها را اجرا می‌کند:
```bash
codesign --force --deep --sign - /path/to/Antigravity\ IDE.app
xattr -dr com.apple.quarantine /path/to/Antigravity\ IDE.app
```
`--sign -` یعنی امضای ad-hoc (بدون Developer ID). این برای اجرای محلی اپلیکیشن کافی است. نیازی به notarization نیست.

نیاز به نصب‌بودن `codesign` است که بخشی از **Xcode Command Line Tools** است:
```bash
xcode-select --install
```

**خطای "Operation not permitted" هنگام پچ**
اگر با این خطا مواجه شدید: `[!] Backup error: [Errno 1] Operation not permitted: '/Applications/Antigravity IDE.app/Contents/Resources/app/out/main.js.bak'`:
1. به ترمینال دسترسی کامل به دیسک بدهید: **تنظیمات سیستم → حریم خصوصی و امنیت → دسترسی کامل به دیسک** (System Settings → Privacy & Security → Full Disk Access).
2. قرنطینه‌ی اپلیکیشن را با دستور زیر بردارید:
   ```bash
   sudo xattr -rd com.apple.quarantine /path/to/Antigravity\ IDE.app
   ```

**اگر اپلیکیشن بعد از پچ اجرا نشد**
1. مطمئن شوید `codesign` در دسترس است: `which codesign`.
2. بررسی کنید `.app` دوباره امضا شده: `codesign -dv /Applications/Antigravity\ IDE.app 2>&1 | grep Authority` — باید `Signature=adhoc` نمایش داده شود.
3. اگر macOS باز هم مسدود می‌کند: در **تنظیمات سیستم → حریم خصوصی و امنیت**، پایین صفحه دکمه‌ی «اجازه‌ی اجرا در هر حال» را خواهید دید.

## ⚙️ پیش‌نیازها
- **Python** نسخه‌ی 3.x
- **وابستگی‌ها:** `packaging` (برای مقایسه‌ی نسخه‌ها)
- **سیستم‌عامل:**
  - **ویندوز** — پشتیبانی کامل از جست‌وجوی خودکار از طریق رجیستری و UAC.
  - **لینوکس** — جست‌وجوی خودکار در `/usr/share/antigravity-ide`، تشخیص نسخه از طریق `dpkg`/`rpm`/`package.json`، ارتقای دسترسی با sudo.
  - **macOS** — جست‌وجوی خودکار در `/Applications/Antigravity IDE.app` و `~/Applications/Antigravity IDE.app`، تشخیص نسخه از طریق `package.json`، امضای مجدد ad-hoc از طریق `codesign` (Xcode Command Line Tools).
- **حداقل نسخه‌ی Antigravity:** `2.0.1`
- **نسخه‌های پشتیبانی‌شده:** `2.0.1` به بالا (با انتخاب نسخه‌محورِ الگوی auth برای `1.23+`)

## 🛠️ Build (ساخت فایل اجرایی)
برای ساخت فایل‌های اجرایی، استفاده از محیط مجازی (virtual environment) توصیه می‌شود. (دستورات کامل برای ویندوز، لینوکس و macOS با pyinstaller در فایل اصلی پروژه، بدون تغییر، موجود است.)

## ساختار پروژه
- `main.py` — نقطه‌ی ورود اصلی پچر (بررسی دسترسی‌ها و اجرای CLI).
- `patcher/` — کد اصلی پچر با معماری ماژولار:
  - `constants.py` — ثابت‌های سراسری، عبارات منظم (regex)، نسخه‌ها و الگوهای تزریق.
  - `cli.py` — رابط کاربری کنسول، منو و پردازش ورودی.
  - `utils/` — ابزارهای کمکی سیستمی (رنگ کنسول، دسترسی ادمین، دسترسی POSIX، هش فایل).
  - `ide/` — منطق جست‌وجو و پچ مستقیم Antigravity IDE (فایل‌های `main.js`).
  - `asar/` — منطق باز/بسته‌کردن آرشیو ASAR و پچ اپلیکیشن Antigravity.
  - `agy/` — منطق جست‌وجو و پچ بایت‌سیگنیچر باینری Antigravity CLI (`agy`/`agy.exe`).
- `requirements.txt` — وابستگی‌های ساخت و اجرا.
- `build.txt` — نمونه دستورات ساخت برای سیستم‌عامل‌های مختلف.
- `icon.ico` — آیکون برای `exe`/`app`.

## 📜 لایسنس
این پروژه تحت لایسنس GPL-3.0 منتشر شده است. متن کامل لایسنس در فایل `LICENSE` موجود است.

