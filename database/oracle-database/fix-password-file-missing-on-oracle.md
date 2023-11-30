# 🍇 Fix Password File Missing on Oracle

{% hint style="info" %}
ในกรณีที่เราทำการ Remote Login บน Oracle ด้วย Privilege DBA มันจะทำการ Authentication กับ Password File ซึ่งถ้าหากหายไป จะทำให้ไม่สามารทำการ Remote Login หรือแม้กระทั่ง Grant Privilege DBA ให้กับ User ได้ จะต้องทำการ Create ใหม่
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Password File ถูกลบไป ทำให้ไม่สามารถ Grant SYSDBA ให้ User ได้
{% endhint %}

```
SQL> grant sysdba to scott ; 
ORA-01994: GRANT failed: password file missing or disabled
```

รวมถึงจะไม่สามารถทำการ Remote Login ด้วย User ที่มี Privilege DBA ได้เช่นเดียวกัน

![](https://codeinsane.files.wordpress.com/2020/07/orapwd-01.png?w=636)

## **Configuration**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* Check User in Password File

{% code title="SQL>" %}
```
select * from v$pwfile_users ;
```
{% endcode %}

```
USERNAME                       SYSDB SYSOP SYSAS
------------------------------ ----- ----- -----
```

* Create Password File

{% code title="$" %}
```
orapwd file=orapwORCL password=sys_password entries=3
```
{% endcode %}

* Check User in Password File Again

{% code title="SQL>" %}
```
select * from v$pwfile_users ;
```
{% endcode %}

```
USERNAME                       SYSDB SYSOP SYSAS
------------------------------ ----- ----- -----
SYS                            TRUE  TRUE  FALSE
```

* Grant SYSDBA to SCOTT

{% code title="SQL>" %}
```
grant sysdba to scott ;
```
{% endcode %}

* Check User in Password File Again

{% code title="SQL>" %}
```
select * from v$pwfile_users ;
```
{% endcode %}

```
USERNAME                       SYSDB SYSOP SYSAS
------------------------------ ----- ----- -----
SYS                            TRUE  TRUE  FALSE
SCOTT                          TRUE  FALSE FALSE
```

* Show Parameter Password

{% code title="SQL>" %}
```
show parameter password ;
```
{% endcode %}

```
NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
remote_login_passwordfile            string      EXCLUSIVE
```

**อ่านเพิ่มเติม** : [https://bit.ly/2XoFWMn](https://bit.ly/2XoFWMn)
