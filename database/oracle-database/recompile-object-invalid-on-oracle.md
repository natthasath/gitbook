# 🥦 Recompile Object Invalid on Oracle

{% hint style="info" %}
โดยปกติการใช้งาน Data Pump ในการ Import Database ซึ่งส่วนใหญ่จะใช้ในกรณีที่เราต้องการ Data ย้อนหลัง หลังจากที่เราทำการ Import Database เรียบร้อยแล้วจะเกิด Object Invalid ตามมา ได้แก่พวก View, Schema ทำให้เราต้องทำการ Recompile Object ถึงจะสามารถใช้งานได้
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

### Solution 1 ( กรณีที่มี Object Invalid ไม่เยอะ )&#x20;

* ทำการตรวจสอบ Object Status

{% code title="SQL>" overflow="wrap" %}
```
select object_name, status from dba_objects where object_type = 'VIEW' and status = 'INVALID' ;
```
{% endcode %}

* ทำการ Recompile Object Invalid

{% code title="SQL>" %}
```
alter view view_name compile ;
```
{% endcode %}

### Solution 2 ( กรณีที่มี Object Invalid เยอะ )

* ทำการตรวจสอบ Object Status โดยใช้ SPOOL ในการ Export Command & Result

{% code title="SQL>" %}
```
spool script.sql 
```
{% endcode %}

{% code title="SQL>" overflow="wrap" %}
```
select ' alter view ' || object_name || ' compile ' from dba_objects where object_type = 'VIEW' and status like 'INVALID' ;
```
{% endcode %}

* ทำการแก้ไขไฟล์ script.sql ให้เหลือกแต่คำสั่ง Recompile Object Invalid

{% code title="$" %}
```
vi script.sql
```
{% endcode %}

```
alter view view_name compile ;
alter view view_name compile ;
alter view view_name compile ;
```

* ทำการรัน SQL Script

{% code title="SQL>" %}
```
@/home/oracle/script.sql
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2zqc34z](https://bit.ly/2zqc34z)
