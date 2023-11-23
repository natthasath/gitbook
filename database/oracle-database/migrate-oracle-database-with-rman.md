# 🧄 Migrate Oracle Database with RMAN

{% hint style="info" %}
การ Migrate Oracle Database ด้วย Recovery Manager ( RMAN ) จะไม่เหมือนกับการ Restore & Recovery Oracle Database ที่ใช้แค่เฉพาะ Backup Set แต่จะใช้ Control File ที่ใช้ในการระบุตำแหน่งของไฟล์ต่าง ๆ และ Parameter File เพื่อใช้ในการกำหนดค่า
{% endhint %}

## **Requirement**

* Create Database with DBCA
* Enable Archive Log
* SCP File Backup

## **Get Started**

* ทำการ Connect Database ด้วย RMAN

{% code title="$" %}
```
rman target /
```
{% endcode %}

* ทำการ Start Database ในโหมด Mount

{% code title="RMAN>" %}
```
startup pfile='/u02/ORCL/pfile-ORCL-20190723.ora' nomount ;
```
{% endcode %}

* ทำการ Restore Control File

{% code title="RMAN>" %}
```
restore controlfile from '/u02/ORCL/cntrl_ORCL_79_1_1014382564' ;
```
{% endcode %}

* ทำการ Mount Database

{% code title="RMAN>" %}
```
alter database mount ;
```
{% endcode %}

* ทำการ Catalog RMAN Backup Set

{% code title="RMAN>" %}
```
catalog start with '/u02/ORCL' ;
```
{% endcode %}

* ทำการ Recovery Database แบบ Full Backup

{% code title="RMAN>" %}
```
restore database ;
```
{% endcode %}

{% code title="RMAN>" %}
```
recover database ;
```
{% endcode %}

* ทำการ Open Database

{% code title="RMAN>" %}
```
alter database open resetlogs ;
```
{% endcode %}

* ทำการตรวจสอบ SCN

{% code title="SQL>" %}
```
select current_scn from v$database ;
```
{% endcode %}

* ทำการ Create SPFILE จาก PFILE

{% code title="SQL>" %}
```
create spfile from pfile='/u02/ORCL/pfile-ORCL-20190723.ora' ;
```
{% endcode %}
