# 🍑 Fix Oracle Date Format

{% hint style="info" %}
ในกรณีที่เราทำการ Run SQL Statement บน Oracle Database แล้วไม่สามารถทำการ Run ได้ เนื่องจาก Date Format ของ SQL Statement ไม่ตรงกับพารามิเตอร์ National Language Support ( NLS ) บน Oracle
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Date Format ของ SQL Statement ไม่ตรงกับพารามิเตอร์ National Language Support ( NLS ) บน Oracle ทำให้ไม่สามารถ Run SQL Statement ได้ ซึ่งมีวิธีแก้ 2 วิธี คือ 1. แก้ไขพารามิเตอร์ NLS\_DATE\_LANGUAGE ของ Session 2. แก้ไข SQL Statement ให้ตรงกับ Date Format
{% endhint %}

{% code title="SQL>" %}
```
select to_date('09 MAR 2020','DD MON RRRR') from dual ;
```
{% endcode %}

```
ORA-01843: not a valid month
```

## **Configuration**

### Solution 1&#x20;

* ทำการแก้ไขพารามิเตอร์ NLS\_DATE\_LANGUAGE

{% code title="SQL>" %}
```
alter session set NLS_DATE_LANGUAGE='ENGLISH'
```
{% endcode %}

### Solution 2&#x20;

* ทำการแก้ไข SQL Statement

{% code title="SQL>" overflow="wrap" %}
```
select to_date('09 MAR 2020','DD MON RRRR','NLS_DATE_LANGUAGE=ENGLISH') from dual ;
```
{% endcode %}

**อ่านเพิ่มเติม** : [http://bit.ly/32ZnvPZ](http://bit.ly/32ZnvPZ)
