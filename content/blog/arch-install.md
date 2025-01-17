---
title: "آموزش نصب آرچ لینوکس"
description: "آموزش نصب توزیع آرچ لینوکس همراه با میزکار XFCE"
image: "images/post/arch-linux-install.jpg"
date: 2023-12-26T12:55:40+03:30
author: "Gnkalk"
tags: ["ArchLinux", "installation"]
categories: ["Linux"]
draft: false
---

نصب آرچ از کار هاییست که بسیاری تا زمانی که آموزش آن جلوی دیدگانشان نباشد توانایی انجام آن را ندارند؛ در این مقاله من قصد دارم به شکل کاملا سنتی و ساده، شما را در نصب آرچ همراهی کنم.

نخستین نکته مورد توجه ای که باید به آن توجه این است که در این آموزش ما آرچ را به همراه میزکار XFCE نصب میکنیم و همچنین شما میتوانید به مراجعه به مقاله « کار هایی که پس از نصب آرچ نیاز به انجام آن دارید! » فرایند آماده بکار کردن آرچ را بهبود بخشید.

دومین نکته قابل توجه نیز این است که این مقاله برای افراد باتجربه مناسب بوده و در صورتی که تجربه کمی دارید سعی کنید تا حد امکان فرایند هایی که طی نصب نیاز به انجام آن است را پیش از بوت فلش‌درایو انجام دهید.

### ۱. ایزوی آرچ را دریافت کنید.
بی‌شک در نخستین مرحله نیاز است شما ایمیج‌ایزوی آرچ را دریافت کنید که برای اینکار تنها لازم به است به وبگاه آرچ رفته و آن را دریافت کنید.

#### ۲. از صحت ایزو مطمئن شوید. (اختیاری)
برای اینکار لازم است ابتدا نرم‌افزار GnuPG را دریافت و سپس با اتکا به آموزش موجود در ویکی آرچ از صحت ایزوی دانلود اطمینان حاصل کنید.

### ۳. برای نصب آماده شوید.
کاربران گنو/لینوکس میتوانند با زدن کامند :

‍`$ lsblk -f`

نام فلش‌درایو خود را بیابند و سپس با بکارگیری کامند dd فلش خود را بوتیبل نمایند.

```
# dd bs=4M status=progress if=arch.iso of=/dev/sdc oflag=sync
```
*بجای arch.iso نشانی دقیق فایل ایزوی دانلودی و بجای /dev/sdc نام فلش‌درایو خود را بگذارید.
سپس ریبوت کرده و با بکارگیری گزینه های بوت دستگاه از فلش‌درایو بوت کنید.

### ۴. اتصال به اینترنت
در اینجا توصیه میشود از کابل لن استفاده کرده و از اتصال با Wifi اجتناب کنید. ( همچنین میتوانید برای راهنمایی در زمینه اتصال با Wifi به مطالب موجود در ویکی ارچ اتکا کنید )

### ۵. پارتیشن بندی کنید.
با بکارگیری ابزار cfdisk به پارتیشن بندی بپردازید. ( برای توضیحات تکمیلی شما میتوانید از ویدئو های موجود استفاده کنید و همچنین توصیه میشود پیش از مرحله سوم این مرحله را در سیستم عامل قبلی خود انجام دهید )

![cfdisk](/images/post/arch-install/1.png)

### ۶. پارتیشن‌ها را فرمت کنید.

شما میتوانید با بهره بردن از دستور mkfs به فرمت کردن پارتیشن ها بپردازید. همچنین ما توصیه میکنیم پارتیشن روت را Btrfs و به این صورت :

```
# mkfs.btrfs /dev/root_partition
```
و سپس پارتیشن هوم را ext4 یا ext3 به این صورت :

```
# mkfs.ext4 /dev/home_partition
```
فرمت کنید؛ در صورتی که نوع پارتیشن بندی شما GPT میباشد بایستی چند مرحله پارتیشن بندی و موارد مربوط به آن را در مقاله دیگری بگذرانید که بعد در وبگاه قرار میگیرند. ( در صورتی که هنگامی که این مقاله را میخوانید آن مقاله قرار نگرفته است میتوانید به ویکی آرچ مراجعه کنید )

### ۷. پارتیشن را ماونت کنید.
برای ماونت پارتیشن روت :

```
# mount  /dev/root_partition /mnt
```
و ماونت پارتیشن هوم :

```
# mount  /dev/home_partition /mnt/home
```
*ممکن است هنگام ماونت کردن پارتیشن هوم خطایی دریافت کنید برای رفع این خطا به مسیر /mnt بروید و یک پوشه با نام home بسازید و دوباره دستور مربوطه را اجرا کنید.

### ۸. بسته های ضروری را نصب کنید.
با بکارگیری pacstrap بسته های ضروری را نصب کنید :

```
# pacstrap /mnt base linux linux-firmware man-db man-pages nano
```

### ۹. فایل fstab را بسازید.
برای تولید فایل fstab می‌بایست از دستور genfstab استفاده کنید :

```
# genfstab -U /mnt >> /mnt/etc/fstab
```

### ۱۰. روت خود را تغییر دهید.
با بهره بری از کامند arch-chroot روت خود را تغییر دهید :

```
# arch-chroot /mnt
```

### ۱۱. لوکال‌فایل را مناسب سازی کنید.
با اجرای نانو :

```
# nano /etc/locale.gen
```
خط "en_US.UTF-8 UTF-8" را از کامنت در بیاورید و سپس دستور :

```
# locale-gen
```
را اجرا و سپس با اجرای نانو :

```
# nano /etc/locale.conf
```
خط "LANG=en_US.UTF-8" را به آن بیافزایید.

### ۱۲. نامی برای دستگاه خود برگزینید.
با اجرای نانو :

```
# nano /etc/hostname
```
یک نام برای دستگاه خود برگزیده و بنویسید، سپس آن را ذخیره و ببندید.

### ۱۳. برای روت گذرواژه برگزینید.
با اجرای دستور passwd و وارد کردن گذرواژه مورد نظر برای روت گذرواژه برگزینید.

### ۱۴. آماده برای بوت..
با دستور :

```
# pacman -S grub
```
بوت‌لودر گراب را نصب و سپس میکروکد پردازنده خود را با بهره گیری از دستورات :

```
# pacman -S intel-ucode (for intel processors)
# pacman -S amd-ucode (for amd processors)
```
نصب کنید، همچنین توصیه میشود دو ابزار os-prober و ntfs-3g را نیز نصب کنید : ( در صورتی که پارتیشن ntfs دارید )

```
# pacman -S os-prober ntfs-3g
```
در نهایت فایل های گراب را تولید :

```
# grub-install ??target=i386-pc /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg
```
و از chroot خارج شده و دستور reboot را وارد کنید ( با دستور exit از chroot خارج شوید )

### ۱۵. زمان را تنظیم کنید.
با بهره گیری از دستورات :

```
# timedatectl set-ntp true
# ln -sf /usr/share/zoneinfo/Asia/Tehran /etc/localtime
# hwclock ??systohc
```
این فرایند را انجام دهید.

### ۱۶. میرور های مناسب را برگزینید.
شما میتوانید با بهره گیری از دستورات زیر :

```
# pacman -S reflector
# reflector ??age 12 ??protocol https ??sort rate ??save /etc/pacman.d/mirrorlist
# pacman -Syy
```
سریع‌ترین میرور های ممکن را برگزینید.

### ۱۷. نصب میزکار XFCE
در نخستین گام لازم است درایور کارت گرافیک شما نصب باشد، پس میتوانید از دستورات زیر بهره بگیرید :

```
# pacman -S xf86-video-amdgpu xf86-video-ati
-- for Nvidia graphic cards --
# pacman -S xf86-video-nouveau
```
و در نهایت نصب میزکار XFCE و لاگین‌منیجر لایت‌دی‌ام :

![XFCE](/images/post/arch-install/2.webp)

```
# pacman -S xorg-server
# pacman -S lightdm lightdm-gtk-greeter lightdm-gtk-greeter-settings
# systemctl enable lightdm
# pacman -S xfce4
# reboot
```

اگر تا اینجا مراحل را به درستی گذرانده باشید حال یک آرچ کامل بر روی دستگاه شما نصب است، همچنین شما میتوانید برای کامل کردن این فرایند به مقاله « کار هایی که پس از نصب آرچ نیاز به انجام آن دارید! » مراجعه کنید.

منبع (https://github.com/alikzmi/archinstall-tutorial)