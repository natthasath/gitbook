# 🎩 Scam Mail

{% hint style="info" %}
หลายคนคงเคยได้รับอีเมลหลอกลวงในรูปแบบต่าง ๆ ซึ่งส่วนใหญ่จะมีรูปแบบที่คล้าย ๆ กัน โดยอาศัยข้อมูลส่วนตัวบน Social Media รวมถึงข้อมูลรั่วไหลจากเว็บไซต์ต่าง ๆ และอาศัยข้อมูล Sensitive Data อย่าง รหัสผ่าน, ภาพลับส่วนตัว มา Blackmail หรือข่มขู่ ว่าสามารถ Hack ข้อมูลของเหยื่อได้
{% endhint %}

## **🧔🏻 Scam Email**

![](https://codeinsane.files.wordpress.com/2021/02/phishing-01.png?w=636\&h=369)

จากอีเมลที่ได้รับ ผู้โจมตีบอกว่าได้โจมตีผ่าน Malware แล้วอ้างว่าสามารถเข้าถึงเครือข่ายและคอมพิวเตอร์ ทำให้สามารถเข้าถึงข้อมูล รวมถึงควบคุมอุปกรณ์ต่าง ๆ เช่น กล้อง, ไมโครโฟน โดยข่มขู่เหยื่อให้จ่ายเงินเป็น Bitcoin ผ่านเลขบัญชี Wallet ที่แนบมา หากเหยื่อไม่มีความเข้าใจมากพอก็จะคิดว่าถูกแฮกจริง ๆ อาจจะทำให้สูญเงินได้

## **👮🏻 Pattern**

* แบบแรก : อาศัยข้อมูล Sensitive Data ที่รั่วไหลจากเว็บไซต์ต่าง ๆ อย่าง รหัสผ่าน, ภาพลับส่วนตัว มา Blackmail หรือข่มขู่ ว่าสามารถ Hack ข้อมูลของเหยื่อได้
* แบบที่สอง : อาศัยการส่งอีเมลไปหาเหยื่อด้วยอีเมลของเหยื่อเอง มา Blackmail หรือข่มขู่ ว่าสามารถ Hack ข้อมูลของเหยื่อได้

## 💂🏻‍♂️ Protect

* แบบแรก : ไม่หลงเชื่อ และทำการเปลี่ยนรหัสผ่านบนบริการทั้งหมด ที่ใช้รหัสผ่านนั้น และทำการเปิดใช้งาน Two-Factor Authentication ส่วนข้อมูล Sensitive Data ควรเปิดเผยข้อมูลเท่าที่จำเป็น และไม่ควรเปิดเป็น Public
* แบบที่สอง : ไม่หลงเชื่อ และทำการแจ้งผู้ดูแลระบบ เพื่อกำหนดค่า Email Setting ให้มีความปลอดภัยตาม Policy ขององค์กร

## **🕵🏻 Email Header Analysis**

การตรวจสอบ Email Header เพื่อใช้ในการหาเส้นทางการรับส่งของอีเมล ถ้าเป็น Microsoft Outlook ให้เข้าไปที่ Mail -> View -> View message detail ส่วน Google ให้เข้าไปที่ Mail -> Show original ซึ่ง Email Header ที่เห็นจะเป็น Text ยาว ๆ ทำให้อ่านลำบาก จะมีเครื่องมือที่ช่วยในการอ่าน Email Header ได้แก่

* [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365)
* [Google Admin Toolbox](https://toolbox.googleapps.com/apps/main/)

![](https://codeinsane.files.wordpress.com/2021/02/phishing-02.png?w=636\&h=320)

## **🧑🏻‍⚖️ Email Setting ( Admin )**

ผู้ดูแลระบบ สามารถตั้งค่าระบบเพื่อป้องกันการส่งอีเมลปลอม และป้องกันการรับอีเมลปลอม ดังนี้

* กำหนด SPF Record ให้ทำการส่งเมลออกจาก Domain ด้วยหมายเลข IP Address ตาม Policy ที่กำหนด แนะนำเป็น

```
-all (Hard Fail) = rejected
~all (Soft Fail) = junk
```

* กำหนด DKIM Record ให้สร้าง Public Key และ Private Key โดยประกาศ Public Key บน DNS Record เพื่อป้องกันการแก้ไขข้อมูลระหว่างทาง
* กำหนด DMARC Record ให้ฝั่งผู้รับดำเนินการกับอีเมลที่ไม่ผ่านการตรวจสอบสิทธิ์ แนะนำเป็น

```
p=reject (Required) = rejected
p=quarantine (Required) = up to you
```

* กำหนด SPF Record สำหรับแต่ละ Subdomain ขององค์กร
* กำหนด SPF Record ( -all ) และ DMARC ( p=reject ) สำหรับ Domain ที่ไม่มีการใช้งาน หรือ Domain ที่ไม่ได้ใช้ในการส่งอีเมล

**อ่านเพิ่มเติม** : [http://bit.ly/3pETYob](http://bit.ly/3pETYob), [https://bit.ly/2NwBJ7r](https://bit.ly/2NwBJ7r)
