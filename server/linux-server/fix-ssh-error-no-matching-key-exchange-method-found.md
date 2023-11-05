# 👿 Fix SSH Error: no matching key exchange method found

{% hint style="info" %}
ในกรณีที่เราทำการ SSH ไปยัง Server แล้วเกิด Error ว่า no matching key exchange method found ทำให้ไม่สามารถเข้าถึง Server ได้ ซึ่งจะเกิดกับ Server ที่ใช้ระบบปฏิบัติการ OS รุ่นเก่าๆ
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก Key Algorithm ที่ใช้ในการแลกเปลี่ยนไม่ตรงกัน ซึ่งจะเกิดกับ Server ที่ใช้ระบบปฏิบัติการ OS รุ่นเก่า ๆ ที่ใช้ Key Algorithm ที่ล้าสมัยไปแล้ว ซึ่งเราสามารถแก้ไขได้โดยการระบุ Key Algorithm ที่จะเชื่อมต่อไปยัง Server โดยดูจาก Error ที่ตอบกลับมา
{% endhint %}

{% code overflow="wrap" %}
```
ssh username#10.10.10.10
---
Unable to negotiate with 10.10.10.10 port 22: no matching key exchange method found. Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1
```
{% endcode %}

## **Configuration**

* ทำการระบุ Key Algorithm ที่ใช้

```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 username#10.10.10.10
```

**อ่านเพิ่มเติม** : [https://bit.ly/3Ywn8cn](https://bit.ly/3Ywn8cn)
