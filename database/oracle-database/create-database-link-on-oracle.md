# 🥬 Create Database Link on Oracle

{% hint style="info" %}
หากใครเคยเขียนโปรแกรมต่อฐานข้อมูลแบบ Multiple Database บน Oracle Database ก็จะมีเทคนิคในการ Connect ระหว่าง 2 Physical Database ด้วย Database Link ทำให้เราสามารถเขียนโปรแกรมต่อฐานข้อมูลได้จาก 1 Logical Database ซึ่งดีกว่าในเรื่องของการจัดการ Privilege ทำให้สามารถเข้าถึง Remote Database ได้โดยไม่ต้องเป็น User บน Remote Database
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

### Solution 1 ( กรณีที่อยู่ภายใน Host เดียวกัน )&#x20;

* ทำการสร้าง Database Link

{% code title="SQL>" overflow="wrap" %}
```
create public database link "link_name" connect to "username" identified by "password" using 'oracle_sid' ;
```
{% endcode %}

* ทำการตรวจสอบ Database Link

{% code title="SQL>" %}
```
select owner, db_link, username, host from dba_db_links order by owner, db_link ;
```
{% endcode %}

```
OWNER     |DB_LINK             |USERNAME            |HOST
----------|--------------------|--------------------|----------
PUBLIC    |LINK_ORCL           |SCOTT               |ORCL

1 rows selected.
```

### Solution 2 ( กรณีที่อยู่คนละ Host )&#x20;

* ทำการกำหนด tnsnames.ora ของ Host ที่ต้องการ Remote

{% code title="$" %}
```
vi $ORACLE_HOME/network/admin/tnsnames.ora
```
{% endcode %}

```
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = lab-drsite.lab.local)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = ORCL)
    )
  )
```

* ทำการทดสอบด้วย TNSPING

{% code title="$" %}
```
tnsping ORCL
```
{% endcode %}

```
TNS Ping Utility for Linux: Version 11.2.0.2.0 - Production on 24-OCT-2019 15:36:16

Copyright (c) 1997, 2010, Oracle.  All rights reserved.

Used parameter files:


Used TNSNAMES adapter to resolve the alias
Attempting to contact (DESCRIPTION = (ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = lab-drsite.lab.local)(PORT = 1521))) (CONNECT_DATA = (SERVICE_NAME = ORCL)))
OK (0 msec)
```

* ทำการสร้าง Database Link

{% code title="SQL>" overflow="wrap" %}
```
create public database link "link_name" connect to "username" identified by "password" using 'oracle_sid' ;
```
{% endcode %}

* กรณีที่ต้องการลบ Database Link

{% code title="SQL>" %}
```
drop public database link link_name ;
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2qFIjNi](https://bit.ly/2qFIjNi)
