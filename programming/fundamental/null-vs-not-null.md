# 🔴 NULL vs NOT NULL

{% hint style="info" %}
ในการออกแบบฐานข้อมูล Database Design หนึ่งในประเด็นที่สำคัญคือการ Define Column ว่าควรเป็นค่า NULL or NOT NULL ซึ่งเป็น Reserved Word ที่ใช้ในการ Identity Column ผ่านทาง Integrity Constraint ถือเป็นกฎ 1 ใน 13 ข้อ ที่อยู่บน [Codd’s 12 Rules](https://en.wikipedia.org/wiki/Codd's\_12\_rules) ของการทำ Relational Database
{% endhint %}

## **Definition**

```
SQL> CREATE TABLE DEPARTMENT (
  DEPARTMENT_ID NUMBER(4) NOT NULL,
  DEPARTMENT_NAME VARCHAR2(20),
  CONSTRAINT dept_pk PRIMARY KEY(DEPARTMENT_ID)
);
```

<details>

<summary>NULL</summary>

จะหมายถึง ไม่มีค่า ( No Value ) หรือ ไม่ทราบข้อมูล ( Unknown Data ) จะไม่เหมือนกับการใส่ ค่าว่าง ( Empty String ) และการใส่เลขศูนย์ ( Zero Value ) หากทำการกำหนดคอลัมน์เป็น NULL จะเป็นการยอมให้สามารถทำการ Insert Data โดยไม่ต้องใส่ค่าในฟิลด์ เฉพาะคอลัมน์ที่กำหนดเป็น NULL

</details>

<details>

<summary>NOT NULL</summary>

จะหมายถึง ต้องมีค่า ( Define Value ) หรือ ต้องมีข้อมูล ( Define Data ) ก็จะตรงข้ามกับ NULL จะถูกใช้ในคอลัมน์ที่ถูกกำหนดเป็น Primary Key ของ Table หากทำการกำหนดคอลัมน์เป็น NOT NULL จะถูกนำมาใช้ในการสร้าง Condition เพราะมีการ Return ค่าแบบ Boolean ( True or False )

</details>

โดยปกติ Database จะกำหนดให้คอลัมน์เป็น NULL เป็นค่า Default หากนำค่า NULL มาใช้กับตัวดำเนินการทางคณิตศาสตร์ Arithmetic Operation หรือเขียน SQL Query โดยใช้ Aggregate Function จะ Return ค่าเป็น NULL เสมอ

## **Criteria**

หลักเกณฑ์ในการเลือกใช้ NULL หรือ NOT NULL สิ่งแรกที่ควรเลือกใช้เป็นเกณฑ์ในการพิจารณาเป็นลำดับแรกเลยคือ Business Logic ของระบบเรา ว่ายอมให้ข้อมูลนั้นเป็น NULL ได้หรือไม่

<details>

<summary>Optional or Required</summary>

ข้อมูลนั้นเป็นข้อมูลเพิ่มเติมหรือเป็นข้อมูลที่จำเป็นต้องกรอกขาดไม่ได้ ซึ่งหากไม่กรอก อาจมีผลทำให้ Business Logic ทำงานต่อไม่ได้ หรือ ทำงานผิดพลาด ก็ควรเลือกใช้ NOT NULL แต่หากเป็นข้อมูลเพิ่มเติม ไม่ต้องกรอกได้ ก็ควรเลือกใช้ NULL

</details>

<details>

<summary>Data in the Future</summary>

ข้อมูลที่ปัจจุบันยังไม่มี แต่สามารถเพิ่มได้ในอนาคต เช่น ตาราง message ที่ใช้ในการส่งเมล ข้อความที่ใช้ในการส่งเมล message\_detail อาจถูกสร้างรอไว้ แต่ยังไม่ได้กำหนด ก็ควรเลือกใช้ NULL ในกรณีนี้ หรือจะเป็น รูปภาพ ที่สามารถใส่เพิ่มเติมหลังจากสร้าง Account

</details>

<details>

<summary>Normalization</summary>

ข้อมูลนั้นควรมีกระบวนการลดความซ้ำซ้อนในการจัดเก็บหรือไม่ หากใน Table ไม่ได้มีการทำ Normalization แล้วเกิด Multiple Duplicate Column เช่น ตาราง Customer เกิด Duplicate Column โดยมีคอลัมน์สั่งซื้อสินค้า 10 คอลัมน์ ( Order1, Order2, …, Order10 ) แต่สั่งซื้อสินค้าแค่ 1 ชึ้น จะเกิดค่า NULL ใน 9 คอลัมน์ที่เหลือ แทนที่จะเก็บค่า NULL ก็ควรทำ Normalization แยกเป็นตาราง Order แล้วใช้ NOT NULL แทน

</details>

&#x20;**อ่านเพิ่มเติม** : [http://bit.ly/2Q2ePCT](http://bit.ly/2Q2ePCT)
