# 🫐 Check Oracle Error Message with OERR

{% hint style="info" %}
การตรวจสอบ Error Message ของ Database บน Oracle ซึ่งเมื่อเราทำการติดตั้ง Oracle Database จะติดตั้ง Utility ที่ช่วยในการอธิบาย Error Message ที่เกิดขึ้น โดยปกติจะดูรายละเอียดของ [Error Message](https://docs.oracle.com/cd/E11882\_01/server.112/e17766/toc.htm) ผ่านทางเว็บ แต่เราสามารถเรียกดูผ่านทาง Command Line ได้เลย
{% endhint %}

## **Syntax**

```
oerr facility error
facility : types of prefixes (ORA, PLS, EXP, etc.)
```

## **Get Started**

* ทำการแสดง Facility List

{% code title="#" %}
```
more $ORACLE_HOME/lib/facility.lis
```
{% endcode %}

* ทำการตรวจสอบ Error Message ด้วย OERR

{% code title="#" %}
```
oerr ora 01034
```
{% endcode %}

```
01843, 00000, "not a valid month"
// *Cause:
// *Action:
```

* กรณีที่รันบน Windows จะต้องทำการเรียกผ่าน JAVA

{% code title="C:\oracle\bin\java" %}
```
oerr ora 01034
```
{% endcode %}

```
01843, 00000, "not a valid month"
// *Cause:
// *Action:
```

**อ่านเพิ่มเติม** : [https://bit.ly/3f9vf6v](https://bit.ly/3f9vf6v)
