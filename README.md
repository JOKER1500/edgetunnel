# 🚀 edgetunnel

این پروژه یک اسکریپت مبتنی بر Cloudflare Workers است که برای تبدیل تنظیمات VLESS به اشتراک‌های قابل استفاده در ابزارهایی مثل Clash و Singbox طراحی شده.

📺 آموزش ویدیویی: [آموزش کامل edgetunnel](https://www.youtube.com/watch?v=tKe9xUuFODA)  
📺 رفع خطای Error 1101: [مشاهده ویدیو](https://www.youtube.com/watch?v=r4uVTEJptdE)  
💬 گروه تلگرام: [@CMLiussss](https://t.me/CMLiussss)

---

## ⚠️ سلب مسئولیت

این پروژه فقط برای اهداف آموزشی، تحقیقاتی و تست‌های امنیتی ارائه شده. استفاده از آن باید مطابق با قوانین کشور شما باشد.  
- نویسنده هیچ مسئولیتی در قبال استفاده غیرقانونی ندارد.  
- استفاده‌کننده باید ظرف ۲۴ ساعت پس از استفاده، کد را حذف کند.  
- با استفاده از این پروژه، شما با شرایط فوق موافقت می‌کنید.

---

## 🔥 هشدار امنیتی

برای جلوگیری از افشای اطلاعات نود، از ارسال تنظیمات واقعی به اشتراک‌ساز عمومی خودداری کنید.  
می‌توانید اشتراک‌ساز شخصی خود را با استفاده از [WorkerVless2sub](https://github.com/cmliu/WorkerVless2sub) راه‌اندازی کنید.

---

## 💡 نحوه استفاده

### ⚙️ نصب روی Cloudflare Workers  
📺 [آموزش ویدیویی](https://www.youtube.com/watch?v=tKe9xUuFODA&t=191s)

1. ساخت Worker جدید در کنسول Cloudflare  
2. کپی کردن محتوای فایل [`_worker.js`](https://github.com/cmliu/edgetunnel/blob/main/_worker.js)  
3. جایگزینی مقدار `userID` در خط ۴ با UUID خودتان  
4. دسترسی به اشتراک از طریق آدرس:
https://[دامنه شما]/[UUID]
و برای فرمت‌های مختلف:
- Base64: `?sub`
- Clash: `?clash`
- Singbox: `?sb`

5. اتصال دامنه سفارشی از طریق تنظیمات Trigger در کنسول Workers

---

### 🛠 نصب از طریق Cloudflare Pages  
📺 [آموزش ویدیویی](https://www.youtube.com/watch?v=tKe9xUuFODA&t=436s)

1. دانلود فایل [main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip)  
2. ساخت پروژه جدید در Pages و آپلود فایل  
3. تعریف متغیر محیطی `UUID`  
## 🔑 جدول متغیرها

| نام متغیر      | مقدار نمونه                                | ضروری | توضیحات فارسی |
|----------------|---------------------------------------------|--------|----------------|
| `UUID`         | `90cd4a77-141a-43c9-991b-08263cfe9c10`      | ✅     | می‌تونی هر مقداری وارد کنی؛ اگر UUID استاندارد نباشه، به UUID پویا تبدیل می‌شه |
| `KEY`          | `token`                                     | ❌     | کلید UUID پویا؛ در صورت استفاده، `UUID` غیرفعال می‌شه |
| `TIME`         | `7`                                         | ❌     | مدت اعتبار UUID پویا (پیش‌فرض: ۷ روز) |
| `UPTIME`       | `3`                                         | ❌     | زمان بروزرسانی UUID (پیش‌فرض: ساعت ۳ صبح به وقت پکن) |
| `SCV`          | `false` یا `0`                              | ❌     | آیا TLS را نادیده بگیریم؟ (پیش‌فرض: فعال است) |
| `PROXYIP`      | `proxyip.cmliussss.net:443`                | ❌     | نود پروکسی جایگزین برای دسترسی به سایت‌های CFCDN (پشتیبانی از چند مقدار با `,` یا خط جدید) |
| `HTTP`         | `user:pass@127.0.0.1:8080` یا `127.0.0.1:8080` | ❌     | پروکسی HTTP برای دسترسی به CFCDN (پشتیبانی از چند مقدار با `,` یا خط جدید) |
| `SOCKS5`       | `user:pass@127.0.0.1:1080` یا `127.0.0.1:1080` | ❌     | پروکسی SOCKS5 برای دسترسی به CFCDN (پشتیبانی از چند مقدار با `,` یا خط جدید) |
| `GO2SOCKS5`    | `blog.cmliussss.com,*.ip111.cn,*google.com` | ❌     | لیست دامنه‌هایی که باید با SOCKS5 یا HTTP باز بشن (با `*` می‌تونی همه رو بفرستی از طریق پروکسی) |
| `NAT64`        | `dns64.cmi.ztvi.org` یا `2001:67c:2960:6464::/96` | ❌     | در صورت خرابی `PROXYIP`، از این DNS64 یا NAT64 استفاده می‌شه |
| `ADD`          | `icook.tw:2053#دامنه بهینه`                | ❌     | دامنه یا IP بهینه TLS (پشتیبانی از چند مقدار با `,` یا خط جدید) |
| `ADDAPI`       | `https://raw.github.../addressesapi.txt`   | ❌     | آدرس API برای دریافت IPهای TLS بهینه |
| `ADDNOTLS`     | `icook.hk:8080#دامنه بهینه`                | ❌     | دامنه یا IP بهینه بدون TLS |
| `ADDNOTLSAPI`  | `https://raw.github.../addressesapi.txt`   | ❌     | آدرس API برای دریافت IPهای بدون TLS |
| `ADDCSV`       | `https://raw.github.../addressescsv.csv`   | ❌     | فایل CSV نتایج تست سرعت IPها |
| `DLS`          | `8`                                         | ❌     | حداقل سرعت قابل قبول برای IPها (بر اساس مقدار عددی) |
| `CSVREMARK`    | `1`                                         | ❌     | شماره ستون مربوط به توضیحات در فایل CSV |
| `TGTOKEN`      | `6894123456:XXXXXXXXXX...`                 | ❌     | توکن ربات تلگرام برای ارسال اعلان |
| `TGID`         | `6946912345`                                | ❌     | شناسه عددی حساب تلگرام دریافت‌کننده |
| `SUB`          | `SUB.cmliussss.net`                         | ❌     | دامنه اشتراک‌ساز شخصی |
| `SUBAPI`       | `SUBAPI.cmliussss.net`                      | ❌     | بک‌اند تبدیل اشتراک برای Clash و Singbox |
| `SUBCONFIG`    | `https://raw.github.../ACL4SSR_Online_Full_MultiMode.ini` | ❌ | فایل تنظیمات اشتراک‌ساز |
| `SUBEMOJI`     | `false`                                     | ❌     | فعال‌سازی ایموجی در اشتراک (پیش‌فرض: فعال) |
| `SUBNAME`      | `edgetunnel`                                | ❌     | نام اشتراک |
| `RPROXYIP`     | `false`                                     | ❌     | اگر `true` باشه، اشتراک‌ساز به‌صورت اجباری IP پروکسی اختصاص می‌ده |
| `URL302`       | `https://t.me/CMLiussss`                    | ❌     | آدرس هدایت 302 برای صفحه اصلی |
| `URL`          | `https://blog.cmliussss.com`               | ❌     | آدرس بازتابی صفحه اصلی |
| `CFPORTS`      | `2053,2096,8443`                            | ❌     | لیست پورت‌های استاندارد Cloudflare |
| `CF_EMAIL`     | `admin@google.com`                          | ❌     | ایمیل حساب Cloudflare برای دریافت آمار درخواست‌ها |
| `CF_APIKEY`    | `1234567890abcdef1234567890abcdef`          | ❌     | کلید API جهانی حساب Cloudflare برای دریافت آمار |

