
# امنیت سرور

### بستن ای پی های کشور کمونیست

ایران اکسس نکنید.
فقط آی‌پی کشورهای چین، روسیه، کوبا، رومانی، قزاقستان، اوکراین و کشورهایی که درخواست‌های زیاد دارند رو ببندید.

[ آموزش جلوگیری از حمله به سرور و ایران اکسس کردن با ۲ روش ساده ](https://www.youtube.com/watch?v=U90a43fTyL0)


[اعمال محدودیت برای دسترسی‌های مشکوک به دامین از طریق کلودفلر](https://telegra.ph/%D8%A7%D8%B9%D9%85%D8%A7%D9%84-%D9%85%D8%AD%D8%AF%D9%88%D8%AF%DB%8C%D8%AA-%D8%A8%D8%B1%D8%A7%DB%8C-%D8%AF%D8%B3%D8%AA%D8%B1%D8%B3%DB%8C%E2%80%8C%D9%87%D8%A7%DB%8C-%D9%85%D8%B4%DA%A9%D9%88%DA%A9-%D8%A8%D9%87-%D8%AF%D8%A7%D9%85%DB%8C%D9%86-%D8%A7%D8%B2-%D8%B7%D8%B1%DB%8C%D9%82-%DA%A9%D9%84%D9%88%D8%AF%D9%81%D9%84%D8%B1-01-14)

### مسدودسازی سایت‌ها و اپلیکیشن‌های ایرانی

سیستم فیلترینگ از روش‌های متنوعی استفاده می‌کند تا بتواند «حدس بزند» یک IP متعلق به پروکسی سرور می‌باشد یا نه. در چین، یکی از روش‌هایی که GFW استفاده می‌کند این است که اگر از یک سرور خارجی درخواستی به سمت سایت‌های داخلی چینی بیاید، آن را مسدود می‌کند. حدس می‌زنیم که در ایران هم از سیستم مشابهی استفاده می‌شود.


[iranxray](https://github.com/iranxray/hope/blob/main/routing.md#%D9%85%D8%B3%D8%AF%D9%88%D8%AF%D8%B3%D8%A7%D8%B2%DB%8C-%D8%A7%D8%B2-%D8%B3%D9%85%D8%AA-%D8%B3%D8%B1%D9%88%D8%B1)


## دوستانی که سرور رایگان منتشر می کنید
سعی کنید rule های امنیتی اضافه کنید تا بتونید کشور رو محدود کنید
کلا از ایران اکسس کردن خوشم نمیاد
ولی مجبوریم به خاطر منابع کم و مشکلاتی که باز گذاشتن این مورد روی سرورهامون داره از دسترسی بقیه کشورها جلوگیری کنیم

![pic](https://pbs.twimg.com/media/GdIlOg-XAAAaR6W?format=jpg&name=small)

### بستن دامنه‌های ایران و چین

برای این کار فقط کافیه این رو به انتهای پیکربندی‌تون اضافه کنید.

```
    "routing": {
        "domainStrategy": "IPOnDemand",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:cn",
                    "geoip:ir"
                ],
                "outboundTag": "block"
            },
            {
                "type": "field",
                "domain": [
                    "geosite:category-porn"
                ],
                "outboundTag": "block"
            }
        ]
    },
```

### مخفی سازی

این روش به تنهایی باعث فیلترشدن دامنه می‌شود.
پهنای باند مصرفی و بات‌های چینی رو هم باید در نظر بگیرید.

پروژهٔ [NginxReverseProxy](https://github.com/Ptechgithub/NginxReverseProxy)

قابلیت‌ها:
- نصب سایت (170 قالب آماده)
- اعمال محدویت ترافیک
- تغییر path 
- تغییر درگاه HTTPS


[ آموزش ایجاد سایت روی دامنه و زیر دامنه با استفاده از انجینیکس ](https://youtu.be/xFMh8F3JGrA?si=SJuNI1hOn2tl4S8i)



### از پورت های دیفالت پنل ها استفاده نکنید

[ اینکارو نکنی سرورت هک میشه! ](https://www.youtube.com/watch?v=Oiag_izb5wk)


## بستن سایت های غیر اخلاقی و پورن

``` json
{ "type": "field", "outboundTag": "blocked","domain": [ "geosite:category-porn" ] } 


"routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "domain": [
          "geosite:category-porn",
        ],
        "outboundTag": "BLOCK",
        "type": "field"
      },
    ]
  },
```



## دریافت گواهینامه SSL (Certificate) برای دامین و ساب‌دامین

[دریافت گواهینامه SSL (Certificate) برای دامین و ساب‌دامین](https://ivpn.pro/how-to/how-to-get-ssl-certificate-for-domain-and-subdomain/)

## افزایش سرعت SSH
معمولا سرعت اتصال به ssh خیلی کمه و  اختلال بالایی داره با ۲راه میتونید تا حد زیادی مشکل رو حل کنید که یکیش عوض کردنه پورت اتصال هستش یکیش عوض کردن نحوه رمزنگاری این پروتکل

```
sudo nano /etc/ssh/sshd_config
```
برای تغییر پورت کافیه قسمت Port رو از کامنت در بیارید و عوضش کنید
و برای تغییر نحوه رمزنگاری این کد رو اضافه کنید:
```
Ciphers aes128-gcm@openssh.com,aes128-ctr
```
(میتونید الگوریتم های دیگرو از گوگل پیدا کرده و تست کنید که کودوم سرعت بهتری دارن)
و درنهایت برای اعمال شدن تغییرات دستور زیر رو میزنیم
```
sudo systemctl restart sshd
```

### اتصال امن و راحت به سرور

برای اتصال به سرور از ای پی ایران استفاده نکنید.
می تونید حتی از این پراکسی ها استفاده کنید.

[ssheasy](https://ssheasy.com/)



### مخفی سازی پنل 

[ GateKeeper راه‌حل مدیریت و امنیت لینک‌های V2ray و VPN ](https://www.youtube.com/watch?v=b0rMI8boAiI)


##  آموزش دایرکت کردن سایت ها و برنامه های ایرانی در تمام دیوایس ها 

[ آموزش دایرکت کردن سایت ها و برنامه های ایرانی در تمام دیوایس ها ](https://www.youtube.com/watch?v=78DKbSuNk30)


## geo-location routing

This is an Enhanced and All-in-One set of geo-location routing files optimized for Iranian users to use in v2ray/xray and all their compatible clients.

[Iran-v2ray-rules](https://github.com/Chocolate4U/Iran-v2ray-rules)

## Iran Hosted Domains

دوست داشتید اینو ببینید جالبه
برای تعریف rule روی برنامه های مختلف توضیح داده
و میتونید ترافیک ایران و خارج رو تفکیک کنید تا نیازی به قطع و وصل وی پی ان برای مراجعه به سایت هایی که روزانه استفاده می کنید نداشته باشید

</br>

بسیاری از سرویس‌ها و دامنه‌های خارج از ایران سانسور و مسدود شده‌اند و باید برای دسترسی به آن‌ها از VPN و Proxy هایی با امنیت بالا استفاده کنیم، جدای از این مسئله دسترسی به بعضی سرویس‌های ایرانی از طریق IP خارجی مسدود شده است. حال برای رد کردن این سرویس ها لیستی از دامنه‌های داخلی را جمع کرده‌ایم تا با اضافه کردن آن‌ به کلاینت‌های مورد استفاده، دیگر نیاز به قطع کردن VPN برای دسترسی به سرویس‌های داخلی نباشد.

[Iran Hosted Domains](https://github.com/bootmortis/iran-hosted-domains?tab=readme-ov-file)


## تمیزی IP

[تست تمیزی IP و هر آنچه در مورد IP تمیز یا فیلتر شده باید بدانید!](https://ivpn.pro/how-to/how-to-test-clean-ip-for-vpn/)


## شناسایی سرورهای کاربران ssh

[markpash.me](https://markpash.me/blog/fa-ssh-key-identity-discovery)


## برای بک آپ کردن کلید ssh باید چه کار کنیم؟

[برای بک آپ کردن کلید ssh باید چه کار کنیم؟](https://twitter.com/markpash/status/1771899769989767342)


# حریم خصوصی در فیلترشکن

در این ویدیو، کاوشی داریم در پیچیدگی‌های #حریم_خصوصی آنلاین در زمان استفاده از #فیلترشکن. برخی از افراد، نگرانی‌هایی در مورد امکان رصد شدن توسط شرکت ارائه دهنده اینترنت‌شان در زمان استفاده از وی‌پی‌ان دارند.  

[twitter](https://twitter.com/PasKoocheh/status/1773040760088133885)



# کانال حدودا یک میلیون نفری، احتمالا در حال پخش فیلترشکن و VPN آلوده به بدافزار هست.

[کانال حدودا یک میلیون نفری، احتمالا در حال پخش فیلترشکن و VPN آلوده به بدافزار هست.](https://threadreaderapp.com/thread/1772902718559936590.html)


# ESSL

اسکریپت ESSL برای ساده‌تر کردن فرآیند دریافت گواهی SSL از طریق روش‌های مختلف و مسیردهی اتوماتیک یا شخصی‌سازی‌شده اون طراحی شده و برای صدور یا تمدید گواهی از Acme، Certbot و Cloudflare api پشتیبانی می‌کنه.

[github](https://github.com/erfjab/ESSL)


# نکاتی مهم در مورد IP

- کشور مبدأ ثبت IP با لوکیشن سرور یکی باشد. اگر هر کدام متفاوت بود؛ برای تعویض به اطلاع پرووایدر برسانید وگرنه در صرافی‌ها، سایت‌ها و اپلیکیشن‌ها لوکیشن شما را اشتباه تشخیص داده و شما را در ارائه سرویس محدود خواهند کرد.
ادامه 

[twitter](https://threadreaderapp.com/thread/1787212029964476790.html)


# VESSL

پروژه  VESSL ( Very Easy SSL ) یک فورک از پروژه ی ESSL نوشته ی عرفان عزیز هست که براتون آماده کردم👀

با این اسکریپت شما به آسانی میتونید گواهی SSL به روش های مختلف دریافت کنید و بلافاصله اونهارو به مسیر های مختلف ( مخصوصا مسیر خاص پنل مرزبان ، یا پنل xui یا هیدیفای(که البته توصیه نمیکنم)) انتقال بدید.

علاوه بر امکانات پروژه اصلی، در VESSL  :

⭐گزینه ای برای حذف بسته ها و گواهی ها اضافه شده.
⭐باگ گزینه انتقال فایل ها در مرزبان برطرف شد.
⭐اشکال Cloudflare API برطرف شد.

🔗  گیت هاب پروژه VESSL 

دستور اجرای آنی:

sudo bash -c "$(curl -sL https://github.com/azavaxhuman/ESSL/raw/main/essl.sh)"

🌟ستاره فراموش نشه
✨ممنون از عرفان

dailydigitalskil معرفی کرده



# اخاذی

توصیه مهم
اگر فرد یا افراد خرابکار و مزاحم با سوءاستفاده از هوش مصنوعی و ویدئوهای دیپ‌فیک، تصویری برهنه از شما یا اطرافیان‌تان ایجاد کرده‌اند و قصد اخاذی از شما دارند، با مراجعه به وبسایت http://stopncii.org و آپلود تصاویر جعلی و اصلی در آن، می‌توانید درخواست کنید این تصاویر از تمامی پلتفرم‌های آنلاین حذف شود.

http://stopncii.org

https://x.com/TavaanaTech/status/1811797735827554675


## leak

به این تصویر نگاه کنید، با وجود اینکه من VPN ترکیه دارم ولی تونست تشخیص بده که از ایران هستم و IP اصلی من چیه.
این در واقع تکنولوژی WebRTC هست که برای ارتباط گرفتن بدون واسطه توی مرورگرها طراحی شده، بدون واسطه یعنی مثلا با دوستتون تماس تصویری مستقیم بگیرید. /

![pic](https://pbs.twimg.com/media/GeLuZHLW8AABnPr?format=png&name=small)

ولی از طرفی باعث نشتی و لو رفتن آی‌پی اصلی هم میشه.
راه‌های زیادی برای برطرف کردنش هست که یکیشون میتونه نصب این اکستنشن روی مرورگر باشه. /۲
https://webextension.org/listing/webrtc-protect.html

check: https://browserleaks.com/webrtc

https://threadreaderapp.com/thread/1865321073274740815.html?utm_campaign=topunroll

##  جلوگیری از لو رفتن IP و لوکیشن اینترنت شما هنگام اتصال به وی پی ان 


https://www.youtube.com/watch?v=tFecNQMWh_I


## روش های پروپاگاندا که ج.ا ازش استفاده زیادی میکنه


حمله شخصی (Ad hominem): حمله کردن به شخصیت فرد (مثلاً اتهام روابط نامشروع یا خیانت به کشور)، به جای رد کردن منطقی افکار و سخنان او.
مثال های زیادی این روزا میبینیم که توسط سایبری ها راه انداخته میشه و چند تا نادان هم پی اش را میگیرند.


https://threadreaderapp.com/thread/1869280325664387429.html



## اسکن کد ناشناس

مستر جرجندی @lisa_loo_who اون عکس سانسور شده رو بهم داد و بعد بررسی دیدم ماجرای این ولت مترو از نظر تکنیکی و فنی خیلی فرق داشته با چیزی که در توئیت قبلی نوشتم. البته اون هم نکات مهم و درستی بود اما به لحاظ فنی این یه روش دیگست و تقریباً ردشم زدم که میگم.

https://threadreaderapp.com/thread/1870243267130077437.html