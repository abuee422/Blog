---
title: "Raspberry Pi Connect: دسترسی از راه دور به رزبری شما از هرکجا که فکرش را بکنید!"
description: "انتشار نسخه آزمایشی رزبری‌پای کانکت و نکات جالب پیرامون آن"
image: "images/post/raspberry-pi-connect-release.png"
date: 2024-05-31T01:00:29+03:30
author: "Gnkalk"
tags: ["Rasbpberry Pi", "Linux", "News"]
categories: ["Linux"]
draft: false
---

دوست دارید به Raspberry Pi خود را از یک رایانه دیگر از طریق هر مرورگر وب دسترسی داشته باشید و از هرکجا که آن را تصور کنید؟

با استفاده از ابزار جدید Raspberry Pi Connect، امکان این کار را دارید!

در روزهای گذشته توسط بنیاد Raspberry Pi اعلام شده است که ابزار Raspberry Pi Connect، دسترسی امن به رزبری‌پای ( البته مشروط به استفاده از آخرین رزبیان ) را فراهم می‌کند؛ آسان‌تر از آنچه فکر می‌کنید...

این تکنولوژی بر پایه VNC و استفاده از ویژگی‌های دسکتاپ از راه دور موجود در X11 پیاده سازی نشده و از ویلند استفاده میکند که اکنون سیستم‌عامل رزبری‌پای نیز از آن استفاده میکند.

Raspberry Pi Connect از WebRTC نقطه به نقطه (P2P) برای برقراری نشست یا همان سشن قابل دسترس از راه دور به وسیله هر مرورگر وبی که ECMAScript 2020 (ES11) را پشتیبانی می‌کند، استفاده می‌کند.

و اگر اتصال مستقیم نقطه به نقطه کار نمی‌کنند، پل مورکور از Raspberry Pi اضافه می‌کند که این ابزار به شما امکان "انتقال امن ترافیک از طریق سرورهای Raspberry Pi Connect با رمزگذاری DTLS" را می‌دهد.

![reaspberry pi connect](/images/post/raspberry-pi-connect-release/1.png)

واقعا عالیه مگر نه؟

استفاده از Raspberry Pi Connect از طریق اتصال نقطه به نقطه رایگان است و اتصال امن از طریق سرور رله میزبانی شده توسط Raspberry Pi است. اما اگر ترافیک از طریق سرور رله بیش از حد بالا ببرد ممکن هست برای کاربران هزینه‌هایی به دنبال داشته باشد، هرچند احتمال بازنگری در زمینه بالاست.

#### نصب Raspberry Pi Connect
اگر Raspberry Pi OS Bookworm را روی Raspberry Pi 5، Raspberry Pi 4 یا Raspberry Pi 400 اجرا می‌کنید، می‌توانید Raspberry Pi Connect را از طریق خط فرمان نصب کنید:
```
sudo apt install rpi-connect
```

با نصب این ابزار، Raspberry Pi خود را مجدد راه‌اندازی کنید. سرویس Connect به طور خودکار زمانی شروع می‌شود که وارد سیستم می‌شوید ( یعنی بطور خودکار در اتواستارت شما قرار می‌گیرد اما با این‌حال اگر آن را غیرفعال کردید هم میتوانید با دستور زیر اجرایش کنید.
```
 systemctl --user start rpi-connect
```

سرانجام، رزبری‌پای خودتان را به حساب رزبری‌پای‌تان متصل کنید. ( این فرآیند مانند سایر اتصال‌های برنامه‌های دسکتاپ به وب خواهد بود )

بعد از آن، می‌توانید از هر نقطه‌ای به رزبری خود ( اگر روشن و به اینترنت وصل شده باشد البته ) با ورود به وب‌سایت connect.raspberrypi.com در هر مرورگر وبی و در هر مکانی، از هر دستگاهی دسترسی داشته باشید.

![reaspberry pi connect](/images/post/raspberry-pi-connect-release/2.png)

##### می‌خواهید بیشتر بدانید؟
در نظر داشته باشید که Raspberry Pi Connect در حال حاضر در حالت بتا است. تجربه ممکن است ناقص باشد، ممکن است باگ‌ها، پایداری، و یا مشکلات تاخیر وجود داشته باشد. اگر کارایی بی‌نقص برای شما حیاتی است، پس شکیبا باشید و منتظر انتشار پایدار باشید.
و در غیر این صورت، شروع به استفاده کنید. :)

برای دریافت اطلاعات بیشتر پیرامون رزبری‌پای کانکت می‌توانید به [مستندات رزبری](https://www.raspberrypi.com/documentation/services/connect.html) مراجعه کنید.

منابع: [!OMG! Linux](https://www.omglinux.com/raspberry-pi-connect-remote-access-via-web/) و [Raspberry Pi Blog](https://www.raspberrypi.com/news/raspberry-pi-connect/)