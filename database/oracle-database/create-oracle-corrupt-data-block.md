# 🍏 Create Oracle Corrupt Data Block

{% hint style="info" %}
ในกรณีที่เกิด Corrupt Data Block บน Oracle เราสามารถทำการ Recovery Data File ได้ จากไฟล์ Backup ของ RMAN ซึ่งเราจะมาจำลองการเกิด Corrupt Data Block ขึ้น ด้วยการ Change Seek ผ่านทาง dd command บน Linux&#x20;
{% endhint %}

## **Requirement**

* Create Database with Sample Schema ( [Schema Diagrams](https://docs.oracle.com/cd/E18283\_01/server.112/e10831/diagrams.htm#G5482) )
* Enable Archive Log

## **Get Started**

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* ทำการ Create Tablespace

{% code title="SQL>" overflow="wrap" %}
```
create tablespace corrupt datafile '/u01/app/oracle/oradata/ORCL/corrupt.dbf' size 100m ;
```
{% endcode %}

* ทำการ Create User Corrupt

{% code title="SQL>" %}
```
create user corrupt identified by corrupt ;
```
{% endcode %}

* ทำการ Change Default Tablespace

{% code title="SQL>" %}
```
alter user corrupt default tablespace corrupt ;
```
{% endcode %}

* ทำการ Grant Privilege

{% code title="SQL>" %}
```
grant create session, resource to corrupt ;
```
{% endcode %}

* ทำการ Connect Database ด้วย User Corrupt

{% code title="SQL>" %}
```
connect corrupt/corrupt ;
```
{% endcode %}

* ทำการ Create Table Employee

{% code title="SQL>" %}
```
create table emp(eno number(30)) ;
```
{% endcode %}

{% code title="SQL>" %}
```
begin
for i in 1..10000
loop
insert into emp values(i) ;
end loop ;
end ;
/
```
{% endcode %}

```
PL/SQL procedure successfully completed.
```

* ทำการ Count Rows ใน Table Employee

{% code title="SQL>" %}
```
select count(*) from emp ;
```
{% endcode %}

```
  COUNT(*)
----------
     10000
```

* ทำการตรวจสอบ Schema

{% code title="RMAN>" %}
```
report schema ;
```
{% endcode %}

* ทำการ Backup Tablespace Corrupt

{% code title="RMAN>" %}
```
backup tablespace corrupt ;
```
{% endcode %}

* ทำการ Query Header Block ใน Table DBA Segment

{% code title="SQL>" %}
```
select header_block from dba_segments where segment_name = 'EMP' ;
```
{% endcode %}

```
HEADER_BLOCK
------------
         130
```

* ทำการ Corrupt Data Block

{% code title="$" %}
```
dd of=/u01/app/oracle/oradata/ORCL/corrupt.dbf bs=8192 conv=notrunc seek=131 << EOF
```
{% endcode %}

```
> testing corruption
> EOF
0+1 records in
0+1 records out
19 bytes (19 B) copied, 0.000231208 s, 82.2 kB/s
```

* ทำการ Flush Buffer Cache

{% code title="SQL>" %}
```
alter system flush buffer_cache ;
```
{% endcode %}

* ทำการ Connect Database ด้วย User Corrupt

{% code title="SQL>" %}
```
connect corrupt/corrupt ;
```
{% endcode %}

* ทำการ Query Data ใน Table Employee จะเห็นว่า Oracle Error

{% code title="SQL>" %}
```
select count(*) from emp ;
```
{% endcode %}

```
select count(*) from emp
                     *
ERROR at line 1:
ORA-01578: ORACLE data block corrupted (file # 6, block # 131)
ORA-01110: data file 6: '/u01/app/oracle/oradata/ORCL/corrupt.dbfcode
```

### Solution 1&#x20;

* ทำการตรวจสอบด้วย Data Recovery Advisor

{% code title="RMAN>" %}
```
list failure ;
```
{% endcode %}

{% code title="RMAN>" %}
```
advise failure ;
```
{% endcode %}

```
List of Database Failures
=========================

Failure ID Priority Status    Time Detected Summary
---------- -------- --------- ------------- -------
182        HIGH     OPEN      27-NOV-20     Datafile 6: '/u01/app/oracle/oradata/ORCL/corrupt.dbf' contains one or more corrupt blocks

analyzing automatic repair options; this may take some time
allocated channel: ORA_DISK_1
channel ORA_DISK_1: SID=133 device type=DISK
analyzing automatic repair options complete

Mandatory Manual Actions
========================
no manual actions available

Optional Manual Actions
=======================
no manual actions available

Automated Repair Options
========================
Option Repair Description
------ ------------------
1      Perform block media recovery of block 131 in file 6
  Strategy: The repair includes complete media recovery with no data loss
  Repair script: /u01/app/oracle/diag/rdbms/orcl/ORCL/hm/reco_4277806215.hm
```

* ทำการ Recovery Data Block

{% code title="RMAN>" overflow="wrap" %}
```
repair failure ;
```
{% endcode %}

```
Strategy: The repair includes complete media recovery with no data loss
Repair script: /u01/app/oracle/diag/rdbms/orcl/ORCL/hm/reco_4277806215.hm

contents of repair script:
   # block media recovery
   recover datafile 6 block 131;

Do you really want to execute the above repair (enter YES or NO)? YES
executing repair script

Starting recover at 27-NOV-20
using channel ORA_DISK_1

channel ORA_DISK_1: restoring block(s)
channel ORA_DISK_1: specifying block(s) to restore from backup set
restoring blocks of datafile 00006
channel ORA_DISK_1: reading from backup piece /u01/app/oracle/fast_recovery_area/ORCL/backupset/2020_11_27/o1_mf_nnndf_TAG20201127T154218_hw1gzc5z_.bkp
channel ORA_DISK_1: piece handle=/u01/app/oracle/fast_recovery_area/ORCL/backupset/2020_11_27/o1_mf_nnndf_TAG20201127T154218_hw1gzc5z_.bkp tag=TAG20201127T154218
channel ORA_DISK_1: restored block(s) from backup piece 1
channel ORA_DISK_1: block restore complete, elapsed time: 00:00:01

starting media recovery
```

### Solution 2&#x20;

* ทำการตรวจสอบด้วย DBVERIFY

{% code title="$" overflow="wrap" %}
```
dbv file=/u01/app/oracle/oradata/ORCL/corrupt.dbf blocksize=8192
```
{% endcode %}

```
DBVERIFY: Release 11.2.0.2.0 - Production on Fri Nov 27 15:53:11 2020

Copyright (c) 1982, 2009, Oracle and/or its affiliates.  All rights reserved.

DBVERIFY - Verification starting : FILE = /u01/app/oracle/oradata/ORCL/corrupt.dbf
Page 131 is marked corrupt
Corrupt block relative dba: 0x01800083 (file 6, block 131)
Bad header found during dbv:
Data in bad block:
 type: 116 format: 5 rdba: 0x20676e69
 last change scn: 0x7075.72726f63 seq: 0x74 flg: 0x69
 spare1: 0x73 spare2: 0x74 spare3: 0xa
 consistency value in tail: 0xaed20601
 check value in block header: 0x6e6f
 block checksum disabled



DBVERIFY - Verification complete

Total Pages Examined         : 12800
Total Pages Processed (Data) : 19
Total Pages Failing   (Data) : 0
Total Pages Processed (Index): 0
Total Pages Failing   (Index): 0
Total Pages Processed (Other): 131
Total Pages Processed (Seg)  : 0
Total Pages Failing   (Seg)  : 0
Total Pages Empty            : 12649
Total Pages Marked Corrupt   : 1
Total Pages Influx           : 0
Total Pages Encrypted        : 0
Highest block SCN            : 1028466 (0.1028466)
```

* ทำการ Recovery Data Block

{% code title="RMAN>" %}
```
blockrecover datafile 6 block 131 ;
```
{% endcode %}

* ทำการ Validate Tablespace

{% code title="RMAN>" %}
```
backup validate tablespace corrupt ;
```
{% endcode %}

### **Solution 3**&#x20;

* ไม่ต้องตรวจสอบเอง ให้ RMAN ทำการ Validate พร้อมทำการ Recovery ไปเลย

{% code title="RMAN>" %}
```
run {
backup validate database ;
blockrecover corruption list ;
}
```
{% endcode %}

* ทำการ Connect Database ด้วย User Corrupt

{% code title="SQL>" %}
```
connect corrupt/corrupt ;
```
{% endcode %}

* ลองทำการ Query Data ใน Table Employee อีกครั้งหนึ่ง

{% code title="SQL>" %}
```
select count(*) from emp ;
```
{% endcode %}

```
  COUNT(*)
----------
     10000
```

**อ่านเพิ่มเติม** : [https://bit.ly/3o32RI6](https://bit.ly/3o32RI6)
