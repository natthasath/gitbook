# 🧿 Export and Import Distro on Windows Subsystem for Linux

{% hint style="info" %}
หลังจากที่ได้ลองติดตั้ง Docker บน Windows Subsystem for Linux ( WSL ) กันไปแล้ว เราจะมาลอง Export and Import Distro บน WSL กันบ้าง
{% endhint %}

## **Requirement**

* Enable Window Subsystem for Linux ( WSL )
* Install Ubuntu 18.04 LTS from Microsoft Store
* Upgrade Windows 10 Version 1903+

## **Get Started**

* ทำการตรวจสอบ Linux Distro บน Windows Subsystem for Linux

{% code title="C:\>" %}
```
wsl --list --all
```
{% endcode %}

```
Windows Subsystem for Linux Distributions:
Ubuntu-18.04
```

* ทำการ Export Distro

{% code title="C:\> " %}
```
wsl --export Ubuntu-18.04 D:\Work\WSL\backup\Ubuntu-18.04.tar
```
{% endcode %}

* ลองทำการเปิดโฟลเดอร์ backup ขึ้นมา

![WSL-01.png](../../.gitbook/assets/wsl-01.png)

* ทำการ Import Distro

{% code title="C:\>" %}
```
wsl --import Ubuntu-18.04 D:\Work\WSL\backup\Ubuntu-18.04.tar
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2qXDoHJ](https://bit.ly/2qXDoHJ)
