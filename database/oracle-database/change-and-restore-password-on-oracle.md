# 🍓 Change and Restore Password on Oracle

{% hint style="info" %}
ในกรณีที่เราทำการ Change Password บน Oracle เราควรจะทำการ Backup Password เดิมของ User นั้นเอาไว้ก่อน ซึ่งหากแก้ไขไปแล้วอาจทำให้ Application ที่ต่ออยู่ใช้งานไม่ได้ ซึ่ง Oracle จะเก็บเป็นค่า Hash ในเวอร์ชั่นเก่าอย่าง 10g และ 11g จะเก็บเป็นเลขฐาน 16 ส่วนเวอร์ชั่นใหม่ ก็จะเก็บเป็นแบบ SHA-1
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* Show Hash

{% code title="SQL>" %}
```
select name, spare4 from sys.user$ where name = 'SYS' ;
```
{% endcode %}

```
NAME  SPARE4
----- ----------------------------------------------------------------------
SYS   S:02F1A0A8CF84BB24114A77F011ED3942CA0BD4F824FCD6CF1CB597E8A7F4
```

* Show Password Version

{% code title="SQL>" %}
```
select username, password_versions from dba_users where username = 'SYS' ;
```
{% endcode %}

```
USERNAME                       PASSWORD
------------------------------ --------
SYS                            10G 11G
```

* Change Password

{% code title="SQL>" %}
```
alter user sys identified by password ;
```
{% endcode %}

* Restore Password

{% code title="SQL>" overflow="wrap" %}
```
alter user sys identified by values 'S:02F1A0A8CF84BB24114A77F011ED3942CA0BD4F824FCD6CF1CB597E8A7F4' ;
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/39eopet](https://bit.ly/39eopet)
