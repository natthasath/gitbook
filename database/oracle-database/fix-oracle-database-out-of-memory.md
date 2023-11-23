# 🥬 Fix Oracle Database Out of Memory

{% hint style="info" %}
ในกรณีที่เราทำการ Create Instance บน Oracle Database แล้วไม่สามารถทำการ Start Database ได้ เนื่องจาก Memory เต็ม ทำให้ไม่สามารถทำการ Allocate Memory สำหรับ SGA เพื่อใช้ในการ Start Database ได้ ซึ่งค่า Parameter ของ Oracle Database อย่าง Memory Target และ Memory Max Target ไม่ควรจะใหญ่กว่า Shared Memory File System ( /dev/shm )
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Memory ไม่เพียงพอสำหรับ SGA ทำให้ไม่สามารถทำการ Start Database ได้ ซึ่งมันถูกจำกัด Memory บน Kernel ของ OS จะแยกส่วนกันกับ Memory Max Target จะต้องทำการ [Configure Kernel Parameter and Resource Limit](https://docs.oracle.com/cd/E11882\_01/install.112/e24326/toc.htm#BHCCADGD)
{% endhint %}

```
ERROR:
ORA-01034: ORACLE not available
ORA-27102: out of memory
Linux-x86_64 Error: 12: Cannot allocate memory
Additional information: 1
Additional information: 10911759
Additional information: 8
Process ID: 0
Session ID: 0 Serial number: 0
```

## **Configuration**

* ทำการตรวจสอบ File System ของ /dev/shm

{% code title="#" %}
```
df -h /dev/shm
```
{% endcode %}

```
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           4.9G   72K  4.9G   1% /dev/shm
```

* ทำการตรวจสอบ Free Memory ( MB ) จะเห็นว่าเหลือ Free อยู่นิดเดียว ควรทำการเพิ่ม Memory

{% code title="#" %}
```
free -m
```
{% endcode %}

```
             total       used       free     shared    buffers     cached
Mem:          7982       7708        274       5991         62       6330
-/+ buffers/cache:       1315       6666
Swap:         4031       1733       2298
```

* ทำการ Mount File System

{% code title="#" %}
```
mount -t tmpfs shmfs -o size=10G /dev/shm
```
{% endcode %}

* ทำการตรวจสอบ File System ของ /dev/shm อีกครั้งหนึ่ง

{% code title="#" %}
```
df -h /dev/shm
```
{% endcode %}

```
Filesystem      Size  Used Avail Use% Mounted on
shmfs            10G  4.5G  5.6G  45% /dev/shm
```

* ทำการ Change Persistant แล้วทำการ Restart

{% code title="#" %}
```
cat /etc/fstab
```
{% endcode %}

```
...
tmpfs                   /dev/shm                tmpfs   size=10g        0 0
...
```

**อ่านเพิ่มเติม** : [https://bit.ly/2kUPwqf](https://bit.ly/2kUPwqf), [https://bit.ly/2mi1LgL](https://bit.ly/2mi1LgL)
