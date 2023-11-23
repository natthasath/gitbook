# 🥒 Monitor Log Switch each Hour of Day on Oracle with SQL\*Plus

{% hint style="info" %}
หากพูดถึง Log ของ Oracle Database ก็จะได้ยินอยู่ 2 คำ ก็คือ Redo Log และ Archive Log ซึ่ง Archive Log ก็เกิดจากข้อมูลที่อยู่ใน Redo Log เต็ม จากการ Commit Transaction จึงนำข้อมูลมาเขียนใน Archive Log นั่นเอง โดย Default จะมีไฟล์ Redo Log อยู่ 3 ไฟล์ด้วยกัน เพื่อสลับการทำงานกรณีไฟล์หนึ่งเต็มจะไปใช้อีกไฟล์แทน
{% endhint %}

## **Get Started**

* ทำการตรวจสอบ Redo Log Status

{% code title="SQL>" %}
```
select group#, status from v$log ;
```
{% endcode %}

```
    GROUP# STATUS
---------- ----------------
         1 INACTIVE
         2 CURRENT
         3 INACTIVE
```

* ทำการ Monitor Log Switch ในแต่ละชั่วโมง

{% code title="SQL>" %}
```
set linesize 150 ;
```
{% endcode %}

{% code title="SQL>" %}
```
select
to_char(first_time,'YYYY-MON-DD') day,
to_char(sum(decode(to_char(first_time,'HH24'),'00',1,0)),'99') "00",
to_char(sum(decode(to_char(first_time,'HH24'),'01',1,0)),'99') "01",
to_char(sum(decode(to_char(first_time,'HH24'),'02',1,0)),'99') "02",
to_char(sum(decode(to_char(first_time,'HH24'),'03',1,0)),'99') "03",
to_char(sum(decode(to_char(first_time,'HH24'),'04',1,0)),'99') "04",
to_char(sum(decode(to_char(first_time,'HH24'),'05',1,0)),'99') "05",
to_char(sum(decode(to_char(first_time,'HH24'),'06',1,0)),'99') "06",
to_char(sum(decode(to_char(first_time,'HH24'),'07',1,0)),'99') "07",
to_char(sum(decode(to_char(first_time,'HH24'),'08',1,0)),'99') "08",
to_char(sum(decode(to_char(first_time,'HH24'),'09',1,0)),'99') "09",
to_char(sum(decode(to_char(first_time,'HH24'),'10',1,0)),'99') "10",
to_char(sum(decode(to_char(first_time,'HH24'),'11',1,0)),'99') "11",
to_char(sum(decode(to_char(first_time,'HH24'),'12',1,0)),'99') "12",
to_char(sum(decode(to_char(first_time,'HH24'),'13',1,0)),'99') "13",
to_char(sum(decode(to_char(first_time,'HH24'),'14',1,0)),'99') "14",
to_char(sum(decode(to_char(first_time,'HH24'),'15',1,0)),'99') "15",
to_char(sum(decode(to_char(first_time,'HH24'),'16',1,0)),'99') "16",
to_char(sum(decode(to_char(first_time,'HH24'),'17',1,0)),'99') "17",
to_char(sum(decode(to_char(first_time,'HH24'),'18',1,0)),'99') "18",
to_char(sum(decode(to_char(first_time,'HH24'),'19',1,0)),'99') "19",
to_char(sum(decode(to_char(first_time,'HH24'),'20',1,0)),'99') "20",
to_char(sum(decode(to_char(first_time,'HH24'),'21',1,0)),'99') "21",
to_char(sum(decode(to_char(first_time,'HH24'),'22',1,0)),'99') "22",
to_char(sum(decode(to_char(first_time,'HH24'),'23',1,0)),'99') "23"
from v$log_history
group by to_char(first_time,'YYYY-MON-DD')
order by day ;
```
{% endcode %}

```
DAY         00  01  02  03  04  05  06  07  08  09  10  11  12  13  14  15  16  17  18  19  20  21  22  23
----------- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- --- ---
2018-DEC-01   1   0   0   0   0   0   1   0   0   0   1   0   0   0   1   0   0   0   1   0   0   0   1   0
2018-DEC-02   0   0   0   1   0   0   1   0   0   0   1   0   0   0   1   0   0   0   0   1   0   0   1   0
2018-DEC-03   0   0   0   0   0   1   0   0   0   0   0   1   0   0   0   0   0   0   1   0   0   0   1   0
2018-DEC-04   1   0   0   0   0   0   0   0   1   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
2018-NOV-28   0   0   0   0   0   0   0   0   0   0   0   3   0   1   0   0   0   0   0   0   0   1   1   0
2018-NOV-29   0   0   0   0   0   0   1   0   0   0   0   0   0   1   0   0   0   0   0   0   1   0   1   0
2018-NOV-30   0   0   1   0   0   0   0   0   0   1   0   0   0   0   0   1   0   0   0   0   0   0   1   0
2019-JUL-30   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   6   0   0   1   0   0   1
2019-JUL-31   0   0   0   0   0   0   0   0   0   0   0   0   0   1   0   0   0   0   0   0   0   0   1   0
```

**อ่านเพิ่มเติม** : [https://bit.ly/2GH1Gut](https://bit.ly/2GH1Gut)
