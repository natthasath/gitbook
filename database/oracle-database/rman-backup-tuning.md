# 🍌 RMAN Backup Tuning

{% hint style="info" %}
การ Tuning Parameter บน Recovery Manager ( RMAN ) จะเป็นการปรับแต่งพารามิเตอร์ที่ใช่ในการ Backup, Restore & Recovery โดย Default จะถูก Disable ไว้ ซึ่งเราสามารทำการ Enable ขึ้นมาใช้งาน รวมถึงการปรับแต่ง Device Type ทั้ง Disk ( Default ) และ SBT ( System Backup to Tape )
{% endhint %}

## **Parameter**

* Backup Optimization : จะข้ามการสำรองไฟล์หากซ้ำกับไฟล์ที่ทำการสำรองไปยัง Device Type ที่ระบุเรียบร้อยแล้ว ซึ่งจะพิจารณาจาก
  1. Data File ต้องตรงกัน ดูจาก DBID, Checkpoint SCN, Creation SCN และ Resetlogs SCN
  2. Archive Log ต้องตรงกัน ดูจาก DBID, Thread, Sequence Number, Resetlogs SCN
  3. Backup Set ต้องตรงกัน ดูจาก DBID, Backup Set Record ID, Stamp
* Control File Auto Backup : จะทำการสำรองไฟล์ Control File โดยอัตโนมัติ หลังจากใช้คำสั่ง RMAN Backup เสร็จ กรณีที่ทำงานอยู่ในโหมด Archive Log จะทำการสำรองไฟล์ Control File โดยอัตโนมัติ หากมีการเปลี่ยนแปลงโครงสร้างฐานข้อมูลที่ส่งผลกระทบต่อ Control File
* Device Type : จะทำการสำรองไฟล์ไปยัง Disk ( Default ) จะไปอยู่ที่ Fast Recovery Area ซึ่งจะต้องดู Logical Block Size ของ Database กับ Physical Block Size ของ Disk ด้วย โดยส่วนใหญ่จะมี Block Size เท่ากับ 512 Bytes ดังนั้น Logical Block Size ก็อาจจะเป็น 2KB, 4KB, 6KB หากต้องการสำรองไฟล์ไปยัง Non Disk จะต้องกำหนดเป็น SBT

## **Get Started**

* ทำการ Connect Database ด้วย RMAN

{% code title="$" %}
```
rman target /
```
{% endcode %}

* ทำการ Enable Backup Optimization

{% code title="RMAN>" %}
```
configure backup optimization on ;
```
{% endcode %}

* ทำการ Enable Control File Auto Backup

{% code title="RMAN>" %}
```
configure controlfile autobackup on ;
```
{% endcode %}

* ทำการ Configure Device Type

{% code title="RMAN>" %}
```
configure default device type to disk ;
```
{% endcode %}

{% code title="RMAN>" %}
```
configure default device type to sbt ;
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3fqCloO](https://bit.ly/3fqCloO)
