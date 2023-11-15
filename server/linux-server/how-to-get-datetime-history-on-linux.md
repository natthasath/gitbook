# 👿 How to get DateTime History on Linux

{% hint style="info" %}
โดยปกติการใช้งาน History ซึงเป็น Command Line ของ Linux จะไม่แสดงรายละเอียดของวันที่และเวลา DateTime แต่เราสามารถกำหนด Format ผ่าน Variable ที่ชื่อ HISTTIMEFORMAT
{% endhint %}

## **Syntax**

```
 %d : day format is DD
 %m : month format is MM
 %y : year format is YYYY
 %F : full format is YYYY-MM-DD
 %T : time format is HH:MM:SS
```

## **Get Started**

* แก้ไขไฟล์ .bash\_profile เพื่อกำหนด HISTTIMEFORMAT ใหม่ ให้แสดง DateTime ด้วย

{% code title="$" %}
```
echo 'export HISTTIMEFORMAT="%F %T: "' >> ~/.bash_profile
```
{% endcode %}

* ทำการตรวจสอบ History

{% code title="$" %}
```
history    
```
{% endcode %}

```
    1  22/01/20 10:01:59 su -
    2  22/01/20 10:02:16 ifconfig
    3  22/01/20 10:02:18 hostname
    4  22/01/20 10:02:21 whoami
    5  22/01/20 10:02:30 df -h
    6  22/01/20 10:02:34 history
```

**อ่านเพิ่มเติม** : [https://bit.ly/38u9v1Y](https://bit.ly/38u9v1Y)
