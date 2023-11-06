# 🧊 Install Veeam Backup & Replication 11 on Windows

{% hint style="info" %}
Veeam Backup & Replication เป็นเครื่องมือที่ใช้ในการทำ Backup & Recovery ของ VM ซึ่งมีมาถึง Version 11 ที่มาพร้อมกับ Feature ใหม่ อย่างเช่น Continuous Data Protection ( CDP ) ทำให้ได้ Near Zero RPO เมื่อเกิดเหตุการณ์ Data Loss ข้อมูลสูญหาย, Ransomware Protection และยังมีเมนู REST API ที่พร้อมให้เรียกใช้งานอีกด้วย
{% endhint %}

## **Requirement**

* Support Windows Server 2008 +

## **Download**

* [Veeam Backup & Replication 11](https://www.veeam.com/backup-replication-new-download.html)

## **Install**

* ติดตั้งจากไฟล์ iso คลิก Install

<figure><img src="../../.gitbook/assets/veeam-01.png" alt=""><figcaption></figcaption></figure>

* เลือก Accept แล้วคลิก Next

<figure><img src="../../.gitbook/assets/veeam-02.png" alt=""><figcaption></figcaption></figure>

* ใส่ License ถ้าไม่มีก็สามารถคลิก Next ต่อไปได้เลย แต่จะเป็นการทดลองใช้งาน 30 วัน

<figure><img src="../../.gitbook/assets/veeam-03.png" alt=""><figcaption></figcaption></figure>

* ระบุ Path ที่ติดตั้ง แล้วคลิก Next

<figure><img src="../../.gitbook/assets/veeam-04.png" alt=""><figcaption></figcaption></figure>

* จำเป็นจะต้องติดตั้ง SQL Server คลิก Install

<figure><img src="../../.gitbook/assets/veeam-05.png" alt=""><figcaption></figcaption></figure>

* คลิก Next

<figure><img src="../../.gitbook/assets/veeam-06.png" alt=""><figcaption></figcaption></figure>

* คลิก Install

<figure><img src="../../.gitbook/assets/veeam-07.png" alt=""><figcaption></figcaption></figure>

* ขั้นตอนการ Install จะนานนิดนึง

<figure><img src="../../.gitbook/assets/veeam-08.png" alt=""><figcaption></figcaption></figure>

* คลิก Finish

<figure><img src="../../.gitbook/assets/veeam-09.png" alt=""><figcaption></figcaption></figure>

* เปิด Veeam Backup & Replication ขึ้นมา แล้วคลิก Connect

<figure><img src="../../.gitbook/assets/veeam-10.png" alt=""><figcaption></figcaption></figure>

* ทำการ Update Component ให้เรียบร้อย แล้วคลิก Finish

<figure><img src="../../.gitbook/assets/veeam-11.png" alt=""><figcaption></figcaption></figure>

* เป็นอันเสร็จเรียบร้อยในการติดตั้ง

<figure><img src="../../.gitbook/assets/veeam-12.png" alt=""><figcaption></figcaption></figure>
