# 🦭 Fix MySQL and MariaDB Error Access Denied for User Root

{% hint style="info" %}
ในกรณีที่เราลืม Root Password ของ MySQL หรือ MariaDB เราจะไม่สามารถ Login เข้าใช้งานได้ แต่เราสามารถทำการ Reset เพื่อเปลี่ยนรหัสผ่าน Root Password ของ MySQL หรือ MariaDB ได้ผ่านทาง Command Line
{% endhint %}

{% hint style="danger" %}
**Cause** :สาเหตุเนื่องมาจากการที่เราลืม Root Password หรือการที่เรามาดูระบบต่อแต่ไม่ทราบ Root Password เพราะคนเก่าไม่ได้ให้ข้อมูลไว้ ทำให้เราจำเป็นต้องทำการ Reset Password
{% endhint %}

## **Configuration**

* ทำการตรวจสอบ Version ของ MySQL

```
mysql --version
```

* หาก Version ของ MySQL < 5.7 ค่า Default Password จะเป็นค่าว่าง Blank

```
mysql -u root
```

* แต่ถ้า Version ของ MySQL >= 5.7 ให้ทำการเปลี่ยน Password ด้วยคำสั่ง

<pre><code><strong>mysqladmin -u root password new_password
</strong></code></pre>

**อ่านเพิ่มเติม** : [http://bit.ly/3gEnNah](http://bit.ly/3gEnNah)
