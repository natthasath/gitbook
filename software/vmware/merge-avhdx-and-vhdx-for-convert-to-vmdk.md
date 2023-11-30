# 🌠 Merge AVHDX and VHDX for Convert to VMDK

{% hint style="info" %}
หลังจากที่เราได้ลอง Convert จาก VMDK มาเป็น VHDX กันแล้ว เราจะมาลอง Convert จาก VHDX มาเป็น VMDK กันบ้าง โดยปกติการสร้าง Virtual Machine บน Hyper-V จะได้ไฟล์มา 2 ไฟล์ คือ AVHDX และ VHDX ซึ่งจะต้องทำการ Merge ทั้ง 2 ไฟล์เข้าด้วยกันก่อนทำการ Convert
{% endhint %}

## **Get Started**

* เปิดโปรแกรม Hyper-V Manager เลือก Action แล้วคลิก Edit Disk

![](../../.gitbook/assets/merge-01.png)

* คลิก Next

![](../../.gitbook/assets/merge-02.png)

* เลือก AVHDX ไฟล์ที่ต้องการ Merge แล้วคลิก Next

![](../../.gitbook/assets/merge-03.png)

* เลือก Merge แล้วคลิก Next

![](../../.gitbook/assets/merge-04.png)

* เลือก To the parent virtual hard disk แล้วคลิก Next

![](../../.gitbook/assets/merge-05.png)

* คลิก Finish

![](https://codeinsane.files.wordpress.com/2019/07/merge-06.png?w=1100)

* จะเห็น File ที่ถูก Merge เรียบร้อยแล้ว ซึ่งเราสามารถนำไป Convert เป็น VMDK ต่อได้

![](../../.gitbook/assets/merge-06.png)

**อ่านเพิ่มเติม** : [https://bit.ly/2GE2FMb](https://bit.ly/2GE2FMb)
