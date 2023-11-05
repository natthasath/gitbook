# ☁ How to Rename all Files in Folder use UUID with Power Automate Desktop

{% hint style="info" %}
ในกรณีที่เราอยากจะทำการ Rename Files ทั้งหมดที่อยู่ใน Folder เมื่อก่อนเราจะต้องเขียน Code อย่างพวก Python แต่ปัจจุบันเราสามารใช้ Power Automate Desktop ในการ Rename Files ทั้งหมดได้แล้ว ซึ่งใช้งานสะดวกมาก
{% endhint %}

## **Get Started**

* ทำการเปิดโปรแกรม Power Automate Desktop แล้วคลิก New flow

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-01.png?w=1024" alt="" height="550" width="1024"><figcaption></figcaption></figure>

* ทำการกำหนดชื่อ Flow name แล้วคลิก Create

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-02.png?w=900" alt="" height="572" width="900"><figcaption></figcaption></figure>

* เลือก Folder -> Get files in folder ทำการกรอก Folder แล้วคลิก Save

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-03.png?w=620" alt="" height="443" width="620"><figcaption></figcaption></figure>

* เลือก Loops -> For each ทำการกรอก Value to iterate แล้วคลิก Save

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-04.png?w=620" alt="" height="334" width="620"><figcaption></figcaption></figure>

* เลือก Scripting -> Run PowerShell script วางในช่อง For each ทำการกรอก PowerShell code to run แล้วคลิก Save

```
(New-Guid | ft -hidetableheaders | out-string).trim()
```

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-05.png?w=620" alt="" height="420" width="620"><figcaption></figcaption></figure>

* เลือก File -> Rename file(s) วางในช่อง For each ต่อจากข้างบน ทำการกรอก File to rename และ New file name แล้วคลิก Save

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-06.png?w=620" alt="" height="501" width="620"><figcaption></figcaption></figure>

* ทำการ Save แล้วคลิก Run

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-07-2.png?w=1024" alt="" height="550" width="1024"><figcaption></figcaption></figure>

* ลองเข้าไปดู Files ใน Folder

<figure><img src="https://codeinsane.files.wordpress.com/2023/10/rename-08.png?w=1024" alt="" height="577" width="1024"><figcaption></figcaption></figure>

**อ่านเพิ่มเติม** : [https://bit.ly/45npewP](https://bit.ly/45npewP)
