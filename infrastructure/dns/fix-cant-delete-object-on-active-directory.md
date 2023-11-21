# 📬 Fix can’t Delete Object on Active Directory

{% hint style="info" %}
ในกรณีที่เราทำการ Delete Object บน Active Directory จะไม่สามารถทำการลบได้ เนื่องจากบน Active Directory จะมีการป้องกันการ Delete Object เป็นค่า Default ของด่านแรก ส่วนด่านที่ 2 ต้องไปเปิด Recycle Bin ซึ่งเป็น Feature ที่มากับ Windows Server 2012 R2
{% endhint %}

![AD-01.png](../../.gitbook/assets/ad-01.png)

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Active Directory จะทำการ Protect Object เพื่อป้องกันการเกิด Accidental Delete จากความผิดพลาดของ Admin เป็นค่า Default ซึ่งถ้าไม่ได้เปิด Recycle Bin หมายความว่า ลบแล้วหายไปเลยไม่สามารถนำกลับมาได้
{% endhint %}

## **Configuration**

* ทำการเปิด Active Directory Users and Computers คลิก View แล้วเลือก Advanced Features

![AD-02.png](../../.gitbook/assets/ad-02.png)

* เลือก Object ที่ต้องการลบ แล้วคลิกขวา Properties

![AD-03.png](../../.gitbook/assets/ad-03.png)

* ทำการ Uncheck Protect object from accidental deletion แล้วคลิก Apply -> OK

![AD-04.png](../../.gitbook/assets/ad-04.png)

* ลองทำการ Delete Object อีกครั้งหนึ่ง

![AD-05.png](../../.gitbook/assets/ad-05.png)

**อ่านเพิ่มเติม** : [https://bit.ly/2YL0kFg](https://bit.ly/2YL0kFg)
