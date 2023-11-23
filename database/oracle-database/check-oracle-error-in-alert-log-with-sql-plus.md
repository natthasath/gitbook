# 🍐 Check Oracle Error in Alert Log with SQL\*Plus

{% hint style="info" %}
การตรวจสอบ Error ของ Database บน Oracle โดยปกติเราสามารถตรวจสอบ Error ที่พบได้จาก Automatic Diagnostic Repository ( ADR ) แต่จะไม่สะดวกในการเรียกดู Error ย้อนหลัง
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

```
sqlplus / as sysdba
```

* ทำการ Find Error ย้อนหลัง 365 วัน

{% code title="SQL>" %}
```
set linesize 150 ;
```
{% endcode %}

{% code title="SQL>" %}
```
col record_id for 9999999 head ID ;
```
{% endcode %}

{% code title="SQL>" %}
```
col message_text for a120 head message ;
```
{% endcode %}

{% code title="SQL>" overflow="wrap" %}
```
select record_id, 
to_char(originating_timestamp,'DD-MON-YYYY HH24:MI:SS') "TIMESTAMP", message_text 
from X$DBGALERTEXT 
where originating_timestamp > systimestamp - 365 and regexp_like(message_text, '(ORA-|error)') order by record_id ;
```
{% endcode %}

```
   ID TIMESTAMP            message
-------- -------------------- -----------------------------
   32109 17-APR-2021 00:00:19 ORA-00060: Deadlock detected.
```

**อ่านเพิ่มเติม** : [https://bit.ly/3pBYJRF](https://bit.ly/3pBYJRF)
