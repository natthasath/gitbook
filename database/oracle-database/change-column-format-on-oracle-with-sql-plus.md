# 🌶 Change Column Format on Oracle with SQL\*Plus

{% hint style="info" %}
โดยปกติการใช้งาน SQL\*Plus ซึ่งเป็น Command Line ของ Oracle จะแสดงผลลัพธ์ในลักษณะของ Table ซึ่งจะมีการกำหนด Size ของ Column เอาไว้ ทำให้กรณีที่ข้อมูลยาวเกิน Size ของ Column จะขึ้นเป็น ### และเราสามารถกำหนดรูปแบบ Format ของ Column ได้อีกด้วย
{% endhint %}

## **Get Started**

* Page Size ( **row per page** ) – Default 14

{% code title="SQL>" %}
```
set pagesize number
```
{% endcode %}

```
Component                           Version         Status
----------------------------------- --------------- ----------
Oracle Enterprise Manager           11.2.0.2.0      VALID
OWB                                 11.2.0.2.0      VALID
Oracle Application Express          3.2.1.00.12     VALID
OLAP Catalog                        11.2.0.2.0      VALID
Spatial                             11.2.0.2.0      VALID
Oracle Multimedia                   11.2.0.2.0      VALID
Oracle XML Database                 11.2.0.2.0      VALID
Oracle Text                         11.2.0.2.0      VALID
Oracle Expression Filter            11.2.0.2.0      VALID
Oracle Rules Manager                11.2.0.2.0      VALID
Oracle Workspace Manager            11.2.0.2.0      VALID

Component                           Version         Status
----------------------------------- --------------- ----------
Oracle Database Catalog Views       11.2.0.2.0      VALID
Oracle Database Packages and Types  11.2.0.2.0      VALID
JServer JAVA Virtual Machine        11.2.0.2.0      VALID
Oracle XDK                          11.2.0.2.0      VALID
Oracle Database Java Packages       11.2.0.2.0      VALID
OLAP Analytic Workspace             11.2.0.2.0      VALID
Oracle OLAP API                     11.2.0.2.0      VALID

18 rows selected.
```

* Line Size ( _**charecter in row**_ ) – Default 80

{% code title="SQL>" %}
```
set linesize number
```
{% endcode %}

```
INSTANCE_NAME
----------------
HOST_NAME
----------------------------------------------------------------
VERSION STATUS
----------------- ------------
ORCL
lab-ora.lab.local
11.2.0.1.0 OPEN
```

* [Column Format](https://docs.oracle.com/cd/B19306\_01/server.102/b14357/ch6.htm) – Default header

{% code title="SQL>" %}
```
col column_name format 99999999999
```
{% endcode %}

```
CURRENT_SCN
-----------
 1.7853E+10
```
