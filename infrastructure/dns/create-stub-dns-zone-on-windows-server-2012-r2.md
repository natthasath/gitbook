# 📦 Create Stub DNS Zone on Windows Server 2012 R2

{% hint style="info" %}
หลังจากที่เราได้ลองติดตั้ง DNS แบบ Workgroup โดยไม่มีบริการ AD DS และทำการสร้าง Primary DNS Zone และ Secondary DNS Zone กันไปเรียบร้อยแล้ว ต่อมาเราจะมาลองสร้าง Stub DNS Zone กัน ซึ่งเป็นรูปแบบ DNS ที่ทำการเก็บ Record ไว้ เฉพาะบางส่วน เหมาะกับกรณีที่เป็น Active Directory
{% endhint %}

## **Requirement**

* Primary DNS Server ( DC2 ) – Allow Zone Transfer
* Stub DNS Server ( DC1 )

## **LAB Diagram**

<figure><img src="../../.gitbook/assets/dns-zone.png" alt="DNS Zone"><figcaption></figcaption></figure>

## **Get Started**

* ทำการเปิด DNS Manager เลือก Forward Lookup Zone แล้วคลิกขวา New Zone

<figure><img src="../../.gitbook/assets/stub-01.png" alt="Stub-01.png"><figcaption></figcaption></figure>

* คลิก Next

<figure><img src="../../.gitbook/assets/stub-02.png" alt="Stub-02.png"><figcaption></figcaption></figure>

* เลือก Stub Zone แล้วคลิก Next ( กรณีที่ไม่ได้ติดตั้ง Active Directory Domain Service จะไม่สามารถใช้ Option สุดท้ายได้ )

<figure><img src="../../.gitbook/assets/stub-03.png" alt="Stub-03.png"><figcaption></figcaption></figure>

* กำหนดชื่อ Zone Name ตาม Diagram ที่ออกแบบไว้ แล้วคลิก Next

<figure><img src="../../.gitbook/assets/stub-04.png" alt="Stub-04.png"><figcaption></figcaption></figure>

* คลิก Next

<figure><img src="../../.gitbook/assets/stub-05.png" alt="Stub-05.png"><figcaption></figcaption></figure>

* ทำการระบุ IP ของเครื่อง DC2 แล้วคลิก Next

<figure><img src="../../.gitbook/assets/stub-06.png" alt="Stub-06.png"><figcaption></figcaption></figure>

* คลิก Finish

<figure><img src="../../.gitbook/assets/stub-07.png" alt="Stub-07.png"><figcaption></figcaption></figure>

* จะแสดง Record SOA และ NS ที่อยู่ใน Stub DNS Zone เพื่อใช้ในการส่งไปถามเครื่องอื่น

<figure><img src="../../.gitbook/assets/stub-08.png" alt="Stub-08.png"><figcaption></figcaption></figure>
