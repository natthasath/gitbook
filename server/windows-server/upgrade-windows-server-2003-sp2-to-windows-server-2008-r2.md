# 👺 Upgrade Windows Server 2003 SP2 to Windows Server 2008 R2

{% hint style="info" %}
ในกรณีที่เราทำการ Upgrade OS บนระบบปฏิบัติการ Windows Server รุ่นเก่าอย่าง 2003 ซึ่ง End-of-Support ไปนานแล้ว โดยระบบปฎิบัติการขั้นต่ำนั้นควรจะเป็น Windows Server 2008 R2 ขึ้นไป เนื่องจากมี Powershell ทำให้เราเขียน Script ได้ง่าย แต่แนะนำให้เป็น Windows Server 2016 หรือ 2019 ไปเลยจะดีกว่า
{% endhint %}

## **✅ Requirement**

* Check Windows Server 2003 SP2
* Check Free Space Disk on Drive C:
* Check OS 32-bit or 64-bit
* [Windows Server 2008 Standard, Enterprise](https://www.microsoft.com/en-us/download/details.aspx?id=5023)

## **🏆 Get Started**

* คลิก Install

![Upgrade-02](../../.gitbook/assets/upgrade-01.png)

* ทำการ Uncheck Help ออก แล้วคลิก Go online to get the latest updates for installation

![Upgrade-03](../../.gitbook/assets/upgrade-02.png)

* ทำการ Uncheck Automatically activate Windows ออก แล้วคลิก Next

![Upgrade-04](../../.gitbook/assets/upgrade-03.png)

* คลิก No

![Upgrade-05](../../.gitbook/assets/upgrade-04.png)

* เลือก Windows Server 2008 Standard (Full Installation) แล้วคลิก Next คำเตือนเลือกให้ตรงกับ Windows Version เดิม ถ้าเป็น Enterprise เลือก Enterprise

![Upgrade-06](../../.gitbook/assets/upgrade-05.png)

* ทำการ Check I accept the license terms แล้วคลิก Next

![Upgrade-07](../../.gitbook/assets/upgrade-06.png)

* กรณีที่ไม่สามารถคลิก Upgrade ได้ อาจเกิดจาก Open Remote Desktop ให้ทำการ Close Connection แล้วไปทำหน้า Console แทน

![Upgrade-08](../../.gitbook/assets/upgrade-07.png)

**อ่านเพิ่มเติม** : [https://bit.ly/3g6ncYx](https://bit.ly/3g6ncYx)
