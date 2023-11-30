# 👿 Fix Ubuntu Package Manager Lock: Could not get lock /var/lib/dpkg/lock

{% hint style="info" %}
ในกรณีที่เราทำการ Ubuntu ผ่านทาง Command Line แล้วไม่สามารถทำการ Update Package หรือ Install Package ได้ ทั้งๆ ที่เราก็ตั้งค่า Network ถูกต้อง สามารถเข้าถึง Internet ได้ ซึ่งอาจเกิดได้จากหลายๆ สาเหตุ
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุอาจเกิดจากกระบวนการ Install หรือ Upgrade ก่อนหน้าถูกขัดจังหวะ จึงทำให้ไฟล์ dpkg ถูก Lock หรืออาจเกิดจากเครื่องมือจัดการ Package อื่นเปิดอยู่ผ่านทาง Graphic Mode พวก Synaptic Package Manager หรือ Ubuntu Software Center ซึ่งเราสามารถแก้ไขได้ด้วยการ Kill Process และ Remove File Lock ทิ้ง
{% endhint %}

{% code overflow="wrap" %}
```
E: Could not get lock /var/cache/apt/archives/lock – open (11: Resource temporarily unavailable)
E: Unable to lock directory /var/cache/apt/archives/
```
{% endcode %}

## **Configuration**

* ทำการ Kill Process

{% code title="#" %}
```
killall apt-get
```
{% endcode %}

* ทำการ Remove Folder Lock

{% code title="#" %}
```
rm /var/lib/dpkg/lock
```
{% endcode %}

{% code title="#" %}
```
rm /var/lib/dpkg/lock-frontend
```
{% endcode %}

{% code title="#" %}
```
rm /var/lib/apt/lists/lock
```
{% endcode %}

{% code title="#" %}
```
rm /var/cache/apt/archives/lock
```
{% endcode %}

* ทำการ Configure ใหม่อีกครั้ง

{% code title="#" %}
```
dpkg --configure -a
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3N4W66w](https://bit.ly/3N4W66w)
