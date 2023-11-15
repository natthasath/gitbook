# 📙 How to delete Permanent SharePoint Site

{% hint style="info" %}
ในกรณีที่เราทำการ Delete SharePoint Site สามารถทำการลบได้จากฝั่งของ Owner Site และทางฝั่งของ SharePoint Global Administrator หลังจากที่ทำการ Delete เรายังสามารถทำการ Restore ได้ ภายใน 93 วัน แต่หากต้องการลบแบบ Permanent จะต้องทำการลบ Office365 Group ก่อน ซึ่งเรายังสามารถทำการ Restore ได้ ภายในใน 30 วัน ซึ่งเราไม่สามารถทำการลบ Office365 Group ได้จากหน้า Microsoft 365 Admin Center เพราะเป็น Object อยู่บน Azure Active Directory
{% endhint %}

## **Get Started**

* เข้าไปที่หน้าเว็บ [http://portal.office.com](http://portal.office.com/)

![Delete-01](../../.gitbook/assets/delete-01.jpg)

* คลิก Admin

![Delete-02](../../.gitbook/assets/delete-02.png)

* คลิก SharePoint

![Delete-03](../../.gitbook/assets/delete-03.png)

* คลิก Delete sites แล้วทำการ Search จะเห็นว่าไม่สามารถคลิก Permanently delete ได้ เนื่องจากต้องทำการลบ Office365 Group บน Azure Active Directory ก่อน

![Delete-04](../../.gitbook/assets/delete-04.png)

* เข้าไปที่หน้าเว็บ [https://portal.azure.com](https://portal.azure.com/) แล้วคลิก Azure Active Directory

![Delete-05](../../.gitbook/assets/delete-05.png)

* คลิก Groups

![Delete-06](../../.gitbook/assets/delete-06.png)

* เลือก Office365 Group แล้วคลิก Delete -> OK

![Delete-07](../../.gitbook/assets/delete-07.png)

* คลิก Deleted groups เลือก Office365 Group แล้วคลิก Delete permanently -> OK

![Delete-08](../../.gitbook/assets/delete-08.png)

**อ่านเพิ่มเติม** : [https://bit.ly/3bCudyw](https://bit.ly/3bCudyw)
