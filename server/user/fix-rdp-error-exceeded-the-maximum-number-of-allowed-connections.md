# 👽 Fix RDP Error Exceeded the Maximum Number of Allowed Connections

{% hint style="info" %}
ในกรณีที่เราทำการ Remote Connection ผ่าน RDP ไปยัง Windows Server 2003 หรือ Windows XP รุ่นเก่า ๆ จะไม่สามารถทำการ Login ด้วย User ที่มีสถานะ Session เป็น Console เพียงอย่างเดียว แต่ไม่มีสถานะ Session เป็น RDP ทำให้จะไม่สามารถทำการ Remote Connection ได้
{% endhint %}

![Fix-01.PNG](../../.gitbook/assets/fix-01.png)

{% hint style="danger" %}
**Cause** :สาเหตุเนื่องมาจาก User บน Windows มีสิทธิ์ Console เพียงอย่างเดียว แต่ไม่มีสิทธิ์ RDP ในการ Remote Connection ทำให้ไม่สามารถ Login ด้วย User นั้นผ่านทาง RDP ได้
{% endhint %}

## **Configuration**

* ทำการตรวจสอบ Session

{% code title="C:\>" %}
```
query session /server:ip_address
```
{% endcode %}

```
 SESSIONNAME       USERNAME                 ID  STATE   TYPE        DEVICE
 console           Administrator             0  Active  wdcon
 rdp-tcp                                 65536  Listen  rdpwd
```

* ทำการเปิด Remote Desktop Connection ด้วยคำสั่ง

{% code title="#" %}
```
mstsc /admin
```
{% endcode %}

* &#x20;กรณีเป็น Windows XP ต่ำกว่า SP3

{% code title="#" %}
```
mstsc /console
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2YoK5BF](https://bit.ly/2YoK5BF)
