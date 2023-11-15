# 👿 Install Kali Linux GUI on Windows Subsystem for Linux

{% hint style="info" %}
หลังจากที่ Microsoft ได้ออก WSL Version 2 ที่ใช้ Full Linux Kernel และ Full System Call Compatible ทำให้สามารถใช้งาน Kali Linux เวอร์ชั่น 2020.3 ที่ออกมาใหม่แบบ GUI ได้ โดยการติดตั้ง Win-Kex ซึ่งเราจะมาลองติดตั้งกัน
{% endhint %}

## **✅ Requirement**

* Enable Window Subsystem for Linux ( WSL )
* Upgrade Windows Subsystem for Linux ( WSL 2 )
* Re-Install Kali Linux Distro

## **🏆 Install**

* ทำการ Update และ Upgrade

{% code title="#" %}
```
apt-get update && apt-get upgrade -y
```
{% endcode %}

* ทำการติดตั้ง Package

{% code title="#" %}
```
apt-get install kali-win-kex -y
```
{% endcode %}

* ทำการแก้ไขไฟล์ /usr/bin/kex ให้ตรงกับค่า X Display

{% code title="#" %}
```
vi /usr/bin/kex
```
{% endcode %}

```
FullScreen=1 127.0.0.1:2
```

* ทำการ Start Service Kex

{% code title="#" %}
```
kex
```
{% endcode %}

* จะแสดง Kali Linux GUI

<figure><img src="../../.gitbook/assets/winkex-01.png" alt=""><figcaption></figcaption></figure>

**อ่านเพิ่มเติม** : [https://bit.ly/3hna1ny](https://bit.ly/3hna1ny)
