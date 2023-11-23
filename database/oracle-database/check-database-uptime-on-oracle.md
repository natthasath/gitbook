# 🍒 Check Database Uptime on Oracle

{% hint style="info" %}
การตรวจสอบ Uptime ของ Database บน Oracle ซึ่งปกติเราจะตรวจสอบ PMON ซึ่งเป็น Background Process ของ Oracle จาก Process Status ที่รันอยู่บน OS แต่เราจะไม่รู้ว่าจริง ๆ แล้ว Process ถูก Start ตั้งแต่เมื่อไหร่ หากทำการตรวจสอบ Uptime ของ OS แล้วไม่ Down แต่อาจเกิดจาก Uptime ของ Database Down ก็ได้
{% endhint %}

## **Get Started**

* ทำการตรวจสอบ Instance Start Time

{% code title="SQL>" overflow="wrap" %}
```
select instance_name, to_char(startup_time,'DD/MM/YYYY HH24:MI:SS') as start_time from v$instance ;
```
{% endcode %}

```
INSTANCE_NAME    START_TIME
---------------- -------------------
ORCL             01/01/2020 00:00:00
```

* ทำการตรวจสอบ History Start Time

{% code title="SQL>" overflow="wrap" %}
```
select instance_name, to_char(startup_time,'DD/MM/YYYY HH24:MI:SS') as start_time from dba_hist_database_instance order by startup_time desc ; 
```
{% endcode %}

```
INSTANCE_NAME    START_TIME
---------------- -------------------
ORCL             01/01/2020 00:00:00
ORCL             01/01/2019 00:00:00
```

* ทำการตรวจสอบ PMON Start Time

{% code title="SQL>" overflow="wrap" %}
```
select database_name, to_char(logon_time,'DD/MM/YYYY HH24:MI:SS') as start_time from v$session where program like '%PMON%' ;
```
{% endcode %}

```
DATABASE_NAME    START_TIME
---------------- -------------------
ORCL             01/01/2020 00:00:00
```

* ทำการตรวจสอบ SID Start Time

{% code title="SQL>" overflow="wrap" %}
```
select database_name, to_char(logon_time,'DD/MM/YYYY HH24:MI:SS') as start_time from v$session where sid=1 ;
```
{% endcode %}

```
DATABASE_NAME    START_TIME
---------------- -------------------
ORCL             01/01/2020 00:00:00
```

* ทำการตรวจสอบ Database Uptime

{% code title="SQL>" %}
```
select
   'HOST_NAME : ' || host_name,
   'INSTANCE_NAME : ' || instance_name,
   'START_TIME : ' || to_char(startup_time,'DD-MON-YYYY HH24:MI:SS') START_TIME,
   'DATABASE_UPTIME : ' || floor(sysdate - startup_time) || ' days(s) ' || trunc( 24*((sysdate-startup_time) - trunc(sysdate-startup_time))) || ' hour(s) ' || mod(trunc(1440*((sysdate-startup_time) - trunc(sysdate-startup_time))), 60) ||' minute(s) ' || mod(trunc(86400*((sysdate-startup_time) - trunc(sysdate-startup_time))), 60) ||' seconds' DATABASE_UPTIME
from sys.v_$instance ;
```
{% endcode %}

```
HOST_NAME : lab-dcsite.lab.local
INSTANCE_NAME : ORCL
START_TIME : 01-JAN-2020 00:00:00
DATABASE_UPTIME : 120 days(s) 3 hour(s) 30 minute(s) 30 seconds
```

**อ่านเพิ่มเติม** : [https://bit.ly/38meNhr](https://bit.ly/38meNhr)
