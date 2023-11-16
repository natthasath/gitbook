# 👿 Change IP and Hostname on Ubuntu 18.04

{% hint style="info" %}
Canonical ได้ทำการเปลี่ยนแปลง Network บน Ubuntu ตั้งแต่เวอร์ชั่น 17.04 ครั้งใหญ่ทำให้การตั้งค่า Network ทำได้ง่ายขึ้น โดยกำหนด Configuration แบบ YAML File ด้วย Netplan ซึ่งมันจะทำการเลือก Renderer Tool ที่เหมาะสม
{% endhint %}

## **Get Started**

* แสดง Network Interface

{% code title="#" %}
```
ifconfig -a
```
{% endcode %}

* ทำการแก้ไขไฟล์ /etc/netplan/01-netcfg.yaml

{% code title="#" %}
```
vi /etc/netplan/01-netcfg.yaml
```
{% endcode %}

```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses: [192.168.1.10/24]
      gateway4: 192.168.1.1
      nameservers:
       addresses: [8.8.8.8, 8.8.4.4]
```

* ทำการ Apply

{% code title="#" %}
```
netplan apply
```
{% endcode %}

* แก้ไขไฟล์ /etc/hosts

{% code title="#" %}
```
vi /etc/hosts
```
{% endcode %}

```
::1             localhost
127.0.0.1       localhost
192.168.1.10    lab-ubuntu.lab.local lab-ubuntu
```

* ทำการกำหนด Hostname

{% code title="#" %}
```
hostnamectl set-hostname lab-ubuntu.lab.local
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/34kNRvg](https://bit.ly/34kNRvg)
