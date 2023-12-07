# 👿 Change Username and UID / GID on Linux

{% hint style="info" %}
โดยปกติหลังจากที่เราสร้าง User เราอาจจะไม่ได้ Fix ค่า UID และ GID ทำให้อาจเกิดความสับสนในการจัดการสิทธิ์และการเข้าถึงทรัพยากรบน Linux เพื่อลดความผิดพลาดเราจะมา Fix ค่า UID และ GID กัน

รวมถึงการเปลี่ยนชื่อ User และ Home Directory
{% endhint %}

## Get Started

* ทำการ Change Username และ Home Directory

{% code title="#" %}
```
usermod -l newname oldname
```
{% endcode %}

{% code title="#" %}
```
usermod -d /home/newname -m newname
```
{% endcode %}

* ทำการ Change UID

{% code title="#" %}
```
usermod -u 1234 devops
```
{% endcode %}

* ทำการ Change GID

{% code title="#" %}
```
groupmod -g 1234 devops
```
{% endcode %}
