# 🍆 Fix Oracle Service handle not Initialized

{% hint style="info" %}
ในกรณีที่เราทำการ Query Data บน Oracle Database แล้วไม่สามารถทำการ Query ได้ เนื่องจาก Service Name ทำการ Connect Database ผิด ทำให้เกิด Service Handle not Initialized ส่งผลให้ไม่สามารถทำการ Query Data รวมถึงการ Start Database และ Shutdown Database ได้
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Service Name ทำการ Connect Database ผิด ทำให้เกิด Service Handle not Initialized หากทำการ Restart Listener แล้วยังไม่หาย อาจะต้องทำการ Kill Process
{% endhint %}

```
SQL> shutdown immediate
ORA-24324: service handle not initialized
ORA-01041: internal error. hostdef extension doesn't exist
```

## **Configuration**

* ทำการตรวจสอบ Process ของ Oracle SID ทั้งหมด

{% code title="$" %}
```
ps -ef | grep $ORACLE_SID
```
{% endcode %}

* ทำการ Kill Process ทั้งหมดของ Oracle SID ที่ต้องการ

{% code title="$" %}
```
ps -ef | grep $ORACLE_SID | grep -v grep | awk '{print $2}' | xargs -i kill -9 {}
```
{% endcode %}

* ทำการ Restart LISTENER

{% code title="$" %}
```
lsnrctl reload LISTENER
```
{% endcode %}

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* ทำการ Start Database อีกครั้งหนึ่ง

{% code title="SQL>" %}
```
startup
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2ShlPwk](https://bit.ly/2ShlPwk)
