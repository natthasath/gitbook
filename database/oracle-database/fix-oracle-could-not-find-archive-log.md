# 🍅 Fix Oracle could not find Archive Log

{% hint style="info" %}
ในกรณีที่เราทำการ Check Process Golden Gate บน Oracle Database แล้วเกิด ABEND ซึ่งอาจเกิดจากหลายสาเหตุ หนึ่งในนั้นคือ Archive Log ถูกลบ ทำให้ไม่สามารถหา Sequence  Number ของ Oracle Database ได้ ส่งผลให้ Process ของ Golden Gate เกิด ABEND
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Archive Log ถูกลบไป ทำให้ไม่สามารถหา Sequence  Number ของ Oracle Database ได้ จะต้องทำการ Restore Archive Log
{% endhint %}

{% code overflow="wrap" %}
```
2020-07-08 08:54:33  ERROR   OGG-00446  Oracle GoldenGate Capture for Oracle, extorcl.prm:  Could not find archived log for sequence 1839
```
{% endcode %}

## **Configuration**

* ทำการตรวจสอบ Process Golden Gate ด้วย GGSCI

{% code title="GGSCI>" %}
```
info all
```
{% endcode %}

```
Program     Status      Group       Lag at Chkpt  Time Since Chkpt
MANAGER     RUNNING
JAGENT      RUNNING
EXTRACT     ABEND       EXTORCL     00:00:00      00:00:03
```

* &#x20;ทำการแสดง Golden Gate Log

{% code title="$" %}
```
cd /u01/app/oracle/product/gg
```
{% endcode %}

{% code title="$" %}
```
tail -100 ggserr.log
```
{% endcode %}

* &#x20;ทำการตรวจสอบ Archive Log

{% code title="$" %}
```
cd /u01/app/oracle/fast_recovery_area/ORCL/archivelog/
```
{% endcode %}

{% code title="$" %}
```
ls 2020_07_08
```
{% endcode %}

```
o1_mf_1_1842_hj9x9brc_.arc
```

* ทำการ Restore Archive Log ด้วย RMAN

{% code title="RMAN>" %}
```
restore archivelog from logseq=1839;
```
{% endcode %}

* ทำการตรวจสอบ Archive Log อีกครั้งหนึ่ง

{% code title="$" %}
```
cd /u01/app/oracle/fast_recovery_area/ORCL/archivelog/
```
{% endcode %}

{% code title="$" %}
```
ls 2020_07_08
```
{% endcode %}

```
o1_mf_1_1839_hj9x9brc_.arc   o1_mf_1_1841_hj9x9brc_.arc
o1_mf_1_1840_hj9x9brc_.arc   o1_mf_1_1842_hj9x9brc_.arc
```

**อ่านเพิ่มเติม** : [https://bit.ly/3e3XaEc](https://bit.ly/3e3XaEc)
