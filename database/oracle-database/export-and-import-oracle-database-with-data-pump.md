# 🥕 Export and Import Oracle Database with Data Pump

{% hint style="info" %}
Data Pump เป็น Utility ของ Oracle Database ที่ใช้ในการ Backup, Restore & Recovery เหมือน RMAN ในลักษณะของ Logical Backup ที่ใช้งานง่ายกว่า และไม่ต้องทำการ Enable Archive Log Mode เหมาะในกรณีที่ไม่สามารถ Shutdown Database เพื่อทำการ Enable Archive Log Mode ได้ แต่ทำงานช้ากว่ามาก และต้องทำการ Create Database ขึ้นมาก่อน
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* ทำการตรวจสอบ Fast Recovery Area จะเห็นว่า Space Limit ถูกใช้จนเต็ม

{% code title="SQL>" overflow="wrap" %}
```
select space_used/1024/1024/1024, space_limit/1024/1024/1024 from v$recovery_file_dest ;
```
{% endcode %}

```
SPACE_USED/1024/1024/1024 SPACE_LIMIT/1024/1024/1024
------------------------- --------------------------
               3.92004061                     3.9375
```

* ทำการเพิ่ม Size ของ Fast Recovery Area

{% code title="SQL>" %}
```
alter system set db_recovery_file_dest_size=30G ;
```
{% endcode %}

* ทำการตรวจสอบ Fast Recovery Area อีกครั้งหนึ่ง

{% code title="SQL>" overflow="wrap" %}
```
select space_used/1024/1024/1024, space_limit/1024/1024/1024 from v$recovery_file_dest ;
```
{% endcode %}

```
SPACE_USED/1024/1024/1024 SPACE_LIMIT/1024/1024/1024
------------------------- --------------------------
               3.92004061                         30
```

* ทำการ Export Data Pump ด้วย SYSDBA

{% code title="$" %}
```
expdp \"/ as sysdba\" dumpfile=orcl.dmp logfile=export_orcl.log full=yes ;
```
{% endcode %}

* ทำการ Create Tablespace ก่อนทำการ Import

{% code title="SQL>" overflow="wrap" %}
```
create tablespace OGGTBS datafile '/u01/app/oracle/oradata/ORCL/oggtbs.dbf' size 100m reuse autoextend on ;
```
{% endcode %}

* ทำการ Import Data Pump ด้วย SYSDBA

{% code title="$" %}
```
impdp \"/ as sysdba\" dumpfile=orcl.dmp logfile=import_orcl.log full=yes ;
```
{% endcode %}

```
Job "SYS"."SYS_IMPORT_FULL_01" completed with 8214 error(s) at 09:43:56
```

* กรณีที่ต้องการเฉพาะบาง Schema

{% code title="$" overflow="wrap" %}
```
expdp system/oracle schemas=orcl dumpfile=orcl.dmp logfile=export_orcl.log ;
```
{% endcode %}

{% code title="$" overflow="wrap" %}
```
impdp system/oracle schemas=orcl dumpfile=orcl.dmp logfile=import_orcl.log table_exists_action=replace ;
```
{% endcode %}

* กรณีที่ต้องการ Export แบบ Overwrite

{% code title="$" overflow="wrap" %}
```
expdp system/oracle schemas=orcl dumpfile=orcl.dmp logfile=export_orcl.log reuse_dumpfiles=y ;
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2m0Vkyo](https://bit.ly/2m0Vkyo), [https://bit.ly/2maBFfW](https://bit.ly/2maBFfW)
