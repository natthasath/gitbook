# 🌺 Fix Mixed Content: The page was loaded over HTTPS

{% hint style="info" %}
ในกรณีที่เราทำ Website ให้เป็น HTTPS แต่ข้อมูลบางส่วนของเว็บไม่ได้เป็น HTTPS ทั้งหมด หมายความว่ามีการ Link ข้อมูลออกไปภายนอกด้วย HTTP ทำให้ Web Browser ขึ้นเตือนมาและบางครั้งอาจทำให้เว็บไม่สามารถใช้งาน Module หรือ Plugin ที่มีการ Link ออกไปภายนอกด้วย HTTP ได้
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจากข้อมูลของ Website ไม่ได้เป็น HTTPS ทั้งหมด ทำให้เกิด Error Mixed Content ขึ้น ซึ่งอาจส่งผลให้ไม่สามารถโหลดหน้าเว็บได้ The page was loaded over HTTPS แต่สามารถโหลดได้ปกติหากทำการเรียกด้วย HTTP
{% endhint %}

## **Configuration**

* ทำการแก้ไขไฟล์ index.html

```
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```

* ทำการแก้ไขไฟล์ wp-config.php (WordPress), configuration.php (Joomla), config.php, index.php

```
header('Content-Security-Policy: upgrade-insecure-requests');
```

* ทำการแก้ไขไฟล์ .htaccess

```
Header add Content-Security-Policy "upgrade-insecure-requests"
```

**อ่านเพิ่มเติม** : [http://bit.ly/3ypqiSW](http://bit.ly/3ypqiSW)
