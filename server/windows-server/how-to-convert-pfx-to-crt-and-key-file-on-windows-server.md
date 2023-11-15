# 👺 How to convert PFX to CRT and KEY File on Windows Server

{% hint style="info" %}
ในกรณีที่เราทำการ Install SSL Certificate จะมี File Format ที่แตกต่างกัน ซึ่งก็จะเหมาะกับ Web Server แต่ละประเภทแตกต่างกันไป จึงทำให้อาจจะต้องมีการ Convert ให้ตรงกับรูปแบบที่เราจะใช้ แต่ก็สามารถ Convert Online ผ่านทาง [SSL Converter](https://ssl.in.th/tools/ssl-converter/)
{% endhint %}

## **SSL Certificate Format**

ใบรับรองความปลอดภัยทางอิเล็กทรอนิกส์บนมาตรฐาน SSL ( Security Socket Layer ) ที่ออกโดย CA ( Certificate Authority ) จะมีรูปแบบของ File Format แบ่งออกเป็น 2 ประเภท ได้แก่ Base64 ( ASCII ) และ Binary ดังนี้

<details>

<summary>Base64</summary>

* PEM Format : เป็นรูปแบบมาตรฐานของ SSL Certificate ที่นิยมใช้กันมากที่สุด โดยจะมีนามสกุล .pem, .crt, .cer, .key เป็นต้น ซึ่งใช้กับ Web Server พวก Apache, IIS

<!---->

* PKCS#7 Format : เป็นรูปแบบมาตรฐานของ SSL Certificate ที่มีมาตรฐานการเข้ารหัสแบบ Cryptographic Message Syntax ( CMS ) โดยจะมีนามสกุล .p7b, .p7c เป็นต้น ใน 1 ไฟล์จะประกอบไปด้วย SSL Certificate, Intermediate CA, Trusted Root CA

</details>

<details>

<summary>Binary</summary>

* DER Format : คล้ายกับ PEM Format โดยจะมีนามสกุล .der, .cer แต่จะใช้กับ Web Server พวก Java Platform

<!---->

* PKCS#12 Format : คล้ายกับ PKCS#7 Format โดยจะมีนามสกุล .pfx, .p12 แต่สามารถเก็บไฟล์ Private Key ได้ด้วย นิยมใช้งานกับ Windows Server เป็นหลัก

</details>

## **Download**

* [OpenSSL on Windows](http://slproweb.com/products/Win32OpenSSL.html)

## **Get Start**

* ทำการ Extract Private Key จากไฟล์ PFX

{% code title="C:\>" %}
```
openssl pkcs12 -in certificate.pfx -nocerts -out encrypted.key
```
{% endcode %}

* ทำการ Extract Public SSL Certificate จากไฟล์ PFX

{% code title="C:\>" %}
```
openssl pkcs12 -in certificate.pfx -clcerts -nokeys -out certificate.crt
```
{% endcode %}

* ทำการ Decrypted Private Key จากไฟล์ Encrypted Private Key

{% code title="C:\>" %}
```
openssl rsa -in encrypted.key -out decrypted.key
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/36aF6WG](https://bit.ly/36aF6WG)
