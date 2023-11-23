# 🌽 Check Version Component on Oracle with SQL\*Plus

{% hint style="info" %}
การตรวจสอบ Version ของ Component บน Oracle ซึ่งเมื่อเราทำการติดตั้ง Oracle Database จะติดตั้ง Component ที่ช่วยในการทำงานมาให้ด้วย เช่น Oracle Enterprise Manager โดยปกติ Version ของ Component จะเป็น Version เดียวกับตอนที่ติดตั้ง Oracle Database ยกเว้น Oracle Application Express
{% endhint %}

**Get Started**

* ทำการตรวจสอบ Version Component

{% code title="SQL>" %}
```
select comp_name, version, status from dba_registry ;
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
Oracle Database Catalog Views       11.2.0.2.0      VALID
Oracle Database Packages and Types  11.2.0.2.0      VALID
JServer JAVA Virtual Machine        11.2.0.2.0      VALID
Oracle XDK                          11.2.0.2.0      VALID
Oracle Database Java Packages       11.2.0.2.0      VALID
OLAP Analytic Workspace             11.2.0.2.0      VALID
Oracle OLAP API                     11.2.0.2.0      VALID

18 rows selected.
```

**อ่านเพิ่มเติม** : [https://bit.ly/2Oykse3](https://bit.ly/2Oykse3)
