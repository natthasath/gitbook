# 🌶 Fix Oracle End-of-File on Communication Channel

{% hint style="info" %}
ในกรณีที่เราทำการ Start Database บน Oracle Database แล้วไม่สามารถทำการ Start Database ได้ เนื่องจาก Archive Log เต็ม ทำให้ไม่สามารถทำการสำรองข้อมูล Archive Log ได้ ส่งผลให้ไม่สามารถทำการ Start Database และ Shutdown Database ได้ แต่สามารถทำการสั่ง Shutdown Abort ได้
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Archive Log เต็ม ทำให้ไม่สามารถทำการ Start Database และ Shutdown Database ได้ สามารถตรวจสอบ Error ที่พบได้จาก Automatic Diagnostic Repository ( ADR ) ซึ่งมีวิธีแก้ 2 วิธี คือ 1. ทำการขยายพื้นที่ Size ของ Archive Log หรือ 2. ปิดการทำงาน Archive Log หากไม่จำเป็นต้องใช้งาน
{% endhint %}

```
SQL> shutdown immediate
ORA-24324: service handle not initialized
ORA-24323: value not allowed
ORA-01089: immediate shutdown in progress - no operations are permitted
```

```
SQL> startup
ORA-03113: end-of-file on communication channel
Process ID: 31834
Session ID: 191 Serial number: 3
```

## **Configuration**

* ทำการตรวจสอบ Diagnostic ด้วย ADR

{% code title="$" %}
```
adrci
```
{% endcode %}

```
ADRCI: Release 11.2.0.2.0 - Production on Wed Sep 25 08:48:30 2019

Copyright (c) 1982, 2009, Oracle and/or its affiliates.  All rights reserved.

ADR base = "/u01/app/oracle"
```

* ทำการแสดง Home Directory กรณีที่ ADR Base ไม่ได้ทำการกำหนดไว้

{% code title="adrci>" %}
```
show homes
```
{% endcode %}

```
ADR Homes:
diag/rdbms/orcl/ORCL
diag/tnslsnr/ol6/listener
diag/clients/user_oracle/host_2630139245_80
diag/clients/user_oracle/host_288324800_80
```

* ทำการระบุ Home Directory

{% code title="adrci>" %}
```
set home diag/rdbms/orcl/ORCL
```
{% endcode %}

* ทำการแสดง Alert Log

{% code title="adrci>" %}
```
show alert -tail 20
```
{% endcode %}

```
ARC1: Becoming the 'no FAL' ARCH
ARC1: Becoming the 'no SRL' ARCH
ARC3 started with pid=23, OS id=24924
ARC2: Becoming the heartbeat ARCH
Errors in file /u01/app/oracle/diag/rdbms/orcl/ORCL/trace/ORCL_ora_24916.trc:
ORA-19815: WARNING: db_recovery_file_dest_size of 4227858432 bytes is 100.00% used, and has 0 remaining bytes available.
************************************************************************
You have following choices to free up space from recovery area:
1. Consider changing RMAN RETENTION POLICY. If you are using Data Guard,
   then consider changing RMAN ARCHIVELOG DELETION POLICY.
2. Back up files to tertiary device such as tape using RMAN
   BACKUP RECOVERY AREA command.
3. Add disk space and increase db_recovery_file_dest_size parameter to
   reflect the new space.
4. Delete unnecessary files using RMAN DELETE command. If an operating
   system command was used to delete files, then use RMAN CROSSCHECK and
   DELETE EXPIRED commands.
************************************************************************
ARCH: Error 19809 Creating archive log file to '/u01/app/oracle/fast_recovery_area/ORCL/archivelog/2019_09_25/o1_mf_1_38_%u_.arc'
Errors in file /u01/app/oracle/diag/rdbms/orcl/ORCL/trace/ORCL_ora_24916.trc:
ORA-16038: log 2 sequence# 38 cannot be archived
ORA-19809: limit exceeded for recovery files
ORA-00312: online log 2 thread 1: '/u02/ORCL/redo02.log'
USER (ospid: 24916): terminating the instance due to error 16038
System state dump requested by (instance=1, osid=24916), summary=[abnormal instance termination].
System State dumped to trace file /u01/app/oracle/diag/rdbms/orcl/ORCL/trace/ORCL_diag_24849.trc
2019-09-25 07:51:49.544000 +07:00
Dumping diagnostic data in directory=[cdmp_20190925075149], requested by (instance=1, osid=24916), summary=[abnormal instance termination].
Instance terminated by USER, pid = 24916
```

* ทำการ Connect Database ด้วย SQL\*Plus

{% code title="$" %}
```
sqlplus / as sysdba
```
{% endcode %}

* ทำการ Shutdown Database

{% code title="SQL>" %}
```
shutdown immediate ;
```
{% endcode %}

```
Database closed.
Database dismounted.
ORACLE instance shut down.
```

* ทำการ Start Database ในโหมด Mount

{% code title="SQL>" %}
```
startup mount ;
```
{% endcode %}

```
ORACLE instance started.

Total System Global Area  722366464 bytes
Fixed Size                  2216864 bytes
Variable Size             545262688 bytes
Database Buffers          167772160 bytes
Redo Buffers                7114752 bytes
Database mounted.
```

### Solution 1&#x20;

* ทำการตรวจสอบ Fast Recovery Area

{% code title="SQL>" %}
```
show parameter db_recovery_file_dest ;
```
{% endcode %}

```
NAME                                |TYPE       |VALUE
------------------------------------|-----------|------------------------------
db_recovery_file_dest               |string     |/u01/app/oracle/fast_recovery_
                                                 area
db_recovery_file_dest_size          |big integer|4032M
```

* ทำการแก้ไข Parameter ของ Fast Recovery Area

{% code title="SQL>" %}
```
alter system set db_recovery_file_dest_size=20G scope=both ;
```
{% endcode %}

* ทำการตรวจสอบ Fast Recovery Area อีกครั้งหนึ่ง

{% code title="SQL>" %}
```
show parameter db_recovery_file_dest ;
```
{% endcode %}

```
NAME                                |TYPE       |VALUE
------------------------------------|-----------|------------------------------
db_recovery_file_dest               |string     |/u01/app/oracle/fast_recovery_
                                                 area
db_recovery_file_dest_size          |big integer|20G
```

### Solution 2

* ทำการตรวจสอบ Archive Log Mode จะเห็นว่า Open Archive Mode อยู่

{% code title="SQL>" %}
```
select log_mode from v$database ;
```
{% endcode %}

```
LOG_MODE
------------
ARCHIVELOG
```

* ทำการ Close Archive Mode

{% code title="SQL>" %}
```
alter database noarchivelog ;
```
{% endcode %}

* ทำการตรวจสอบ Archive Log Mode อีกครั้งหนึ่ง

{% code title="SQL>" %}
```
select log_mode from v$database ;
```
{% endcode %}

```
LOG_MODE
------------
NOARCHIVELOG
```

* ทำการ Start Database ในโหมด Open

{% code title="SQL>" %}
```
alter database open ;
```
{% endcode %}

```
Database altered.
```

**อ่านเพิ่มเติม** : [https://bit.ly/2l4sNYW](https://bit.ly/2l4sNYW), [https://bit.ly/2lDl04z](https://bit.ly/2lDl04z)
