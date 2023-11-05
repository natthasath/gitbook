# 👿 Fix Ubuntu Package Manager Lock: Could not get lock /var/lib/dpkg/lock

{% hint style="info" %}
ในกรณีที่เราทำการ Ubuntu ผ่านทาง Command Line แล้วไม่สามารถทำการ Update Package หรือ Install Package ได้ ทั้งๆ ที่เราก็ตั้งค่า Network ถูกต้อง สามารถเข้าถึง Internet ได้ ซึ่งอาจเกิดได้จากหลายๆ สาเหตุ
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุอาจเกิดจากกระบวนการ Install หรือ Upgrade ก่อนหน้าถูกขัดจังหวะ จึงทำให้ไฟล์ dpkg ถูก Lock หรืออาจเกิดจากเครื่องมือจัดการ Package อื่นเปิดอยู่ผ่านทาง Graphic Mode พวก Synaptic Package Manager หรือ Ubuntu Software Center ซึ่งเราสามารถแก้ไขได้ด้วยการ Kill Process และ Remove File Lock ทิ้ง
{% endhint %}

```
E: Could not get lock /var/cache/apt/archives/lock – open (11: Resource temporarily unavailable)
E: Unable to lock directory /var/cache/apt/archives/
```

## **Configuration**

* ทำการ Kill Process

```
killall apt-get
```

* ทำการ Remove Folder Lock

```
rm /var/lib/dpkg/lock
```

```
rm /var/lib/dpkg/lock-frontend
```

```
rm /var/lib/apt/lists/lock
```

```
rm /var/cache/apt/archives/lock
```

* ทำการ Configure ใหม่อีกครั้ง

```
dpkg --configure -a
```

**อ่านเพิ่มเติม** : [https://bit.ly/3N4W66w](https://bit.ly/3N4W66w)
