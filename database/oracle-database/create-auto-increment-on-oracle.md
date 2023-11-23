# 🥝 Create Auto Increment on Oracle

{% hint style="info" %}
ในกรณีที่เราทำการ Create Table แล้วต้องการกำหนด Auto Incremental บน Oracle จะไม่เหมือนกับ Database ทั่ว ๆ ไป อย่าง MySQL หรือ SQL Server ที่แค่เลือก Checkbox ก็เสร็จแล้ว แต่บน Oracle จะต้องสร้าง Sequence เพื่อใช้บอกลำดับ ร่วมกับ Trigger ในการดัก Event Insert แล้วทำการหา Next Value ของ Sequence
{% endhint %}

## **Get Started**

* ทำการ Create Table

{% code title="SQL>" %}
```
CREATE TABLE DEPARTMENT (
  DEPARTMENT_ID NUMBER(4) NOT NULL,
  DEPARTMENT_NAME VARCHAR2(20),
  CONSTRAINT dept_pk PRIMARY KEY(DEPARTMENT_ID)
);
```
{% endcode %}

* ทำการ Create Sequence

{% code title="SQL>" %}
```
CREATE SEQUENCE dept_seq START WITH 1;
```
{% endcode %}

* ทำการ Create Trigger

{% code title="SQL>" %}
```
CREATE OR REPLACE TRIGGER dept_trig
  BEFORE INSERT ON DEPARTMENT
  FOR EACH ROW
BEGIN
  SELECT dept_seq.nextval
  INTO :new.DEPARTMENT_ID
  FROM dual;
END;
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3a8Wmxh](https://bit.ly/3a8Wmxh)
