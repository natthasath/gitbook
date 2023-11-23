# 🥕 Check Database Size on Oracle with SQL\*Plus

{% hint style="info" %}
การตรวจสอบ Size ของ Tablespace บน Oracle หากใครเป็น DBA จะต้องหมั่นตรวจสอบทุกวัน เพื่อป้องกันไม่ให้มันเต็ม ซึ่งโดย Default ตอนสร้าง Tablespace จะทำการ Enable Auto Extend ให้อยู่แล้ว นอกจากนี้ยังอาจจะต้องดูพวก Size ของ Data File ด้วย
{% endhint %}

> dba\_data\_files = dba\_segments + dba\_free\_space + Oracle Overhead

## **Get Started**

* Check File Size of Controlfile

{% code title="SQL>" %}
```
select (block_size * file_size_blks)/1024/1024 size_in_mb from v$controlfile ;
```
{% endcode %}

```
SIZE_IN_MB
----------
   9.28125
   9.28125
```

* Check File Size of Archive Log

{% code title="SQL>" %}
```
select trunc(completion_time) archived_date,
    thread#,
    sum(blocks * block_size) / 1024 / 1024 size_in_mb
from v$ARCHIVED_LOG
group by trunc(completion_time), thread#
order by 1, 2 ;
```
{% endcode %}

```
ARCHIVED_    THREAD# SIZE_IN_MB
--------- ---------- ----------
27-JUL-19          1 283.052734
28-JUL-19          1 288.331543
29-JUL-19          1 243.663086
30-JUL-19          1  246.49707
31-JUL-19          1 165.133789
```

* Check Total Size of Data File

{% code title="SQL>" %}
```
select sum(bytes)/1024/1024 size_in_mb from dba_data_files ;
```
{% endcode %}

```
SIZE_IN_MB
----------
      1205
```

* Check Used Size of Data File

{% code title="SQL>" %}
```
select sum(bytes)/1024/1024 size_in_mb from dba_segments ;
```
{% endcode %}

```
SIZE_IN_MB
----------
 1164.3125
```

* Check Free Size of Data File

{% code title="SQL>" %}
```
select sum(bytes)/1024/1024 size_in_mb from dba_free_space ;
```
{% endcode %}

```
SIZE_IN_MB
----------
   36.6875
```

* Check Database Size of Data File Full

{% code title="SQL>" %}
```
select "Total MB" - "Free MB" "Used MB", 
    "Free MB", 
    "Total MB", 
    round(100 * ("Free MB" / "Total MB")) "Pct. Free"
from ( select
  (select sum(bytes/(1014*1024)) from dba_data_files) "Total MB",
  (select sum(bytes/(1024*1024)) from dba_free_space) "Free MB"
from dual );
```
{% endcode %}

```
   Used MB    Free MB   Total MB  Pct. Free
---------- ---------- ---------- ----------
1180.19613    36.6875 1216.88363          3
```

* Check Database Size of Tablespace

{% code title="SQL>" fullWidth="false" %}
```
select tablespace_name, sum(bytes)/1024/1024 Size_MB 
from dba_segments group by tablespace_name order by tablespace_name ;
```
{% endcode %}

```
TABLESPACE_NAME         SIZE_MB
-------------------- ----------
SYSAUX                  460.625
SYSTEM                  664.875
UNDOTBS1                   38.5
USERS                     .3125
```

* Check Database Size of Tablespace Full

{% code title="SQL>" %}
```
select df.tablespace_name "Tablespace",
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
```
{% endcode %}

```
Tablespace              Used MB    Free MB   Total MB  Pct. Free
-------------------- ---------- ---------- ---------- ----------
SYSAUX                      461         29        490          6
SYSTEM                      665          5        670          1
UNDOTBS1                     39          1         40          3
USERS                         0          5          5        100
```

**อ่านเพิ่มเติม** : [https://bit.ly/2ZpGMr6](https://bit.ly/2ZpGMr6), [https://bit.ly/32YOzhK](https://bit.ly/32YOzhK), [https://bit.ly/2Yfzxpk](https://bit.ly/2Yfzxpk)
