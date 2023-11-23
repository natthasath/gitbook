# 🍉 Best Practice Check Tablespace Size on Oracle

{% hint style="info" %}
โดยปกติการตรวจสอบ Tablespace Size บน DBA\_TABLESPACE\_USAGE\_METRICS จะรวมพื้นที่ Block ของการ Auto Extend เข้าไปด้วย ซึ่งจะไม่ตรงกับ Size ที่ใช้อยู่ในปัจจุบัน ซึ่งจะต้องตรวจสอบ Tablespace Size บน DBA\_DATA\_FILES จะเหมาะกับ Auto Extend มากกว่า
{% endhint %}

{% hint style="danger" %}
**Cause** : เกิดจากการตรวจสอบ Tablespace Size แบบผิดวิธี หากไม่ได้เปิด Auto Extend การตรวจสอบบน DBA\_TABLESPACE\_USAGE\_METRICS เป็นวิธีการที่ถูกต้อง แต่หากเปิด Auto Extend ควรจะตรวจสอบบน DBA\_DATA\_FILES
{% endhint %}

```
SQL> select a.tablespace_name "Tablespace",
    round((a.used_space * b.block_size)/1024/1024, 2) as "Used MB",
    round(((a.tablespace_size - a.used_space) * b.block_size)/1024/1024, 2) as "Free MB",
    round((a.tablespace_size * b.block_size)/1024/1024, 2) as "Total MB",
    round(100 - a.used_percent, 2) as "Pct. Free"
from dba_tablespace_usage_metrics a join dba_tablespaces b
    on a.tablespace_name = b.tablespace_name
order by a.tablespace_name ;

Tablespace              Used MB    Free MB   Total MB  Pct. Free
-------------------- ---------- ---------- ---------- ----------
SYSAUX                   463.94   32304.05   32767.98      98.58
SYSTEM                   665.88   32102.11   32767.98      97.97
TEMP                          1   32766.98   32767.98        100
UNDOTBS1                   3.69    32764.3   32767.98      99.99
USERS                      1.31   32766.67   32767.98        100
```

## **Solution**

* ทำการตรวจสอบ Tablespace บน DBA\_DATA\_FILES

```
SQL> select df.tablespace_name "Tablespace",
    totalusedspace "Used MB",
    (df.totalspace - tu.totalusedspace) "Free MB",
    df.totalspace "Total MB",
    round(100 * ((df.totalspace - tu.totalusedspace) / df.totalspace)) "Pct. Free"
from 
    (select tablespace_name, round(sum(bytes) / 1048576) TotalSpace 
        from dba_data_files group by tablespace_name) df,
    (select round(sum(bytes)/(1024*1024)) totalusedspace, tablespace_name 
        from dba_segments group by tablespace_name) tu
where df.tablespace_name = tu.tablespace_name
order by df.tablespace_name ;

Tablespace              Used MB    Free MB   Total MB  Pct. Free
-------------------- ---------- ---------- ---------- ----------
SYSAUX                      461         29        490          6
SYSTEM                      665          5        670          1
UNDOTBS1                     39          1         40          3
USERS                         0          5          5        100
```

**อ่านเพิ่มเติม** : [https://bit.ly/319VUwb](https://bit.ly/319VUwb)
