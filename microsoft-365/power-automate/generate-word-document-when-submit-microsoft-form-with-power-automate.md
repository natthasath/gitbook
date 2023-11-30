# 🤖 Generate Word Document when Submit Microsoft Form with Power Automate

{% hint style="info" %}
หลังจากที่เราได้ลองสร้าง Condition บน Microsoft Flow เพื่อใช้ในการแจ้งเตือนผ่าน Email โดยการใช้ Trigger กันไปแล้ว เราจะมาลองทำแบบฟอร์มออนไลน์ Online Form ซึ่งการ Approve สามารถเขียน Condition ให้ทำการ Approve ผ่าน Email ได้ แต่หัวหน้าต้องการให้ปริ้นเป็นเอกสารได้ด้วย ซึ่งผมก็ไม่เข้าใจจะเก็บหลายที่ทำไม ในเมื่อจะลดใช้กระดาษแล้ว
{% endhint %}

## **Requirement**

* Install Microsoft Office
* Create SharePoint Site
* Create Microsoft Form

## **Get Started**

* เข้าไปที่หน้าเว็บ [http://portal.office.com](http://portal.office.com/)

![](../../.gitbook/assets/form-01.jpg)

* คลิก SharePoint Application เลือก SharePoint Site ที่เราสร้าง

![](../../.gitbook/assets/form-02.png)

### Step 1&#x20;

* ทำการสร้าง Group Column เพื่อทำการนำไป Mapping ค่าในแบบฟอร์ม Word Document  กับ SharePoint List คลิก Settings เลือก Site contents

![](<../../.gitbook/assets/form-03 (1).png>)

* คลิก Site settings

![](../../.gitbook/assets/form-04.png)

* คลิก Site columns

![](../../.gitbook/assets/form-05.png)

* คลิก Create

![](../../.gitbook/assets/form-06.png)

* ทำการกำหนดชื่อ Column Name และ Group แล้วคลิก OK

![](../../.gitbook/assets/form-07.png)

* จะแสดงข้อมูล Group Column

![](../../.gitbook/assets/form-08.png)

### Step 2&#x20;

* ทำการสร้าง SharePoint List เพื่อทำการเก็บข้อมูลที่ถูก Submit จาก Microsoft Form คลิก New เลือก List

![](../../.gitbook/assets/form-09.png)

* ทำการกำหนดชื่อ List Name แล้วคลิก Create

![](../../.gitbook/assets/form-10.png)

* คลิก Add from existing site columns

![](../../.gitbook/assets/form-11.png)

* เลือก FormGroup -> Add Column ที่ต้องการ แล้วคลิก OK

![](../../.gitbook/assets/form-12.png)

* จะแสดงข้อมูล Group Column ที่ถูกเพิ่มเข้ามาใน List

![](../../.gitbook/assets/form-13.png)

### Step 3&#x20;

* ทำการสร้าง Document Library สำหรับเก็บเฉพาะแบบฟอร์ม Word Document คลิก New เลือก Document Library

![](../../.gitbook/assets/form-14.png)

* ทำการกำหนดชื่อ Document Library แล้วคลิก Create

![](../../.gitbook/assets/form-15.png)

* คลิก Add from existing site columns

![](../../.gitbook/assets/form-16.png)

* เลือก FormGroup -> Add Column ที่ต้องการ แล้วคลิก OK

![](../../.gitbook/assets/form-17.png)

### Step 4&#x20;

* ทำการสร้าง Word Document คลิก New แล้วเลือก Word document

![](../../.gitbook/assets/form-18.png)

* คลิก Open in Desktop App

![](../../.gitbook/assets/form-19.png)

* คลิก Insert -> Quick Parts -> Document Property -> แล้วเลือก Column ใน Column Group ที่สร้าง

![](../../.gitbook/assets/form-20.png)

### Step 5&#x20;

* ทำการสร้าง Flow คลิก Power Automate Application

![](../../.gitbook/assets/form-21.png)

* คลิก Create เลือก Automated Flow

![](../../.gitbook/assets/form-22.png)

* ทำการกำหนดชื่อ Flow name โดยระบุ Trigger เป็น When an item is created ( SharePoint ) แล้วคลิก Create <mark style="color:red;">คำเตือนชื่อต้องมากกว่า 3 ตัวขึ้นไป</mark>

![](../../.gitbook/assets/form-23.png)

* ทำการกรอก Site Address และ List Name แล้วคลิก Next step

![](../../.gitbook/assets/form-24.png)

* เลือก Get file content ทำการกรอก Site Address และ File Identifier แล้วคลิก Next step

![](../../.gitbook/assets/form-25.png)

* เลือก Create file ทำการกรอก Site Address, Folder Path, File Name, File Content แล้วคลิก Next step

![](../../.gitbook/assets/form-26.png)

* เลือก Update file properties ทำการกรอก Site Address, Library Name และ Column จาก FormList มาใส่ใน FormDocument

![](../../.gitbook/assets/form-27.png)

* คลิก Test เลือก I’ll perform the trigger action คลิก Safe & Test แล้วคลิก Run flow <mark style="color:red;">คำเตือนต้องใส่ข้อมูลใน FormList ก่อน Flow ถึงจะทำการ Run ได้</mark>

![](../../.gitbook/assets/form-28.png)

### Step 6&#x20;

* ทำการใส่ข้อมูลใน FormList คลิก New กรอกรายละเอียดของ User Request แล้วคลิก Save <mark style="color:red;">คำเตือนข้อมูลใน FormList จะถูก Submit มาจาก Microsoft Form แต่จะทำการลองใส่ข้อมูลให้ดูก่อน</mark>

![](../../.gitbook/assets/form-29.png)

* จะแสดงข้อมูล Word Document ที่ถูก Generate มาจาก User Request เมื่อทำการ Submit จาก Microsoft Form

![](../../.gitbook/assets/form-30.png)

* ทำการเปิดไฟล์ Word แบบ Open in app <mark style="color:red;">คำเตือนหากทำการเปิดไฟล์ Word แบบ Open in browser จะไม่เห็นข้อมูล</mark>

![](../../.gitbook/assets/form-31.png)

**อ่านเพิ่มเติม** : [http://bit.ly/3d1sILy](http://bit.ly/3d1sILy)
