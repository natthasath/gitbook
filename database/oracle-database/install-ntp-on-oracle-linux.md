# 🍌 Install NTP on Oracle Linux

{% hint style="info" %}
NTP ( Network Time Protocol ) เป็นโปรโตคอลที่ใช้ในการ Sync Time ของเครื่อง Server ทุกเครื่องภายใน Network ให้ตรงกันผ่าน Protocol UDP ซึ่งทำงานแบบ Client-Server หรือ Peer-to-Peer ด้วย Port 123 ถ้าหาก Sync Time ของเครื่องไม่ตรงกัน อาจจะทำให้ Application หรือ Database ทำงานผิดพลาดได้&#x20;
{% endhint %}

## **Install**

* ทำการติดตั้ง Package

{% code title="#" %}
```
yum install ntp -y
```
{% endcode %}

* ทำการแก้ไขไฟล์ /etc/ntp.conf เลือกตาม [NTP Pool Zone in Thailand](https://www.pool.ntp.org/zone/th) คำเตือนหากไม่ระบุ iburst จะไม่ทำการ Sync ทันที ดังนั้นควรระบุ

{% code title="#" %}
```
vi /etc/ntp.conf
```
{% endcode %}

```
server 3.th.pool.ntp.org iburst
server 0.asia.pool.ntp.org iburst
server 2.asia.pool.ntp.org iburst
```

* กรณีที่ต้องการใช้ NTP Server อื่นของไทย

{% code title="#" %}
```
vi /etc/ntp.conf
```
{% endcode %}

```
server time.navy.mi.th iburst
server time1.nimt.or.th iburst
server clock.nectec.or.th iburst
```

* ทำการ Enable Firewall

{% code title="#" %}
```
iptables -I INPUT -p udp -m udp --dport 123 -j ACCEPT
```
{% endcode %}

{% code title="#" %}
```
service iptables save
```
{% endcode %}

* ทำการ Start Service NTP

{% code title="#" %}
```
service ntpd restart
```
{% endcode %}

* ทำการกำหนดให้ Start ทุกครั้งที่ Restart เครื่อง

{% code title="#" %}
```
chkconfig ntpd on
```
{% endcode %}

* ทำการตรวจสอบ List of Peers ด้วย NTP Query

{% code title="#" %}
```
ntpq -pn
```
{% endcode %}

```
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 203.147.59.16   .INIT.          16 u    -   64    0    0.000    0.000   0.000
 110.78.24.101   .IRIG.           1 u    -   64    1    3.513    0.018   0.000
 203.185.67.115  .GPS.            1 u    -   64    1    2.370    0.093   0.000
```

* ทำการแสดง Network Time Synchronization ด้วย NTP Stat

{% code title="#" %}
```
ntpstat
```
{% endcode %}

```
synchronised to NTP server (218.186.3.36) at stratum 2
   time correct to within 75 ms
   polling server every 64 s
```

* ทำการตรวจสอบ Date

{% code title="#" %}
```
date
```
{% endcode %}

```
Fri Nov 13 17:17:29 +07 2020
```

* ทำการสร้าง Crontab

{% code title="#" %}
```
crontab -e
```
{% endcode %}

{% code overflow="wrap" %}
```
0 0 * * * root /usr/sbin/ntpdate -s -u time.navy.mi.th time1.nimt.or.th clock.nectec.or.th
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/38E7ROy](https://bit.ly/38E7ROy), [https://bit.ly/35tDSaq](https://bit.ly/35tDSaq)
