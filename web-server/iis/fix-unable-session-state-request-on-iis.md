# 🦺 Fix Unable Session State Request on IIS

{% hint style="info" %}
ในกรณีที่เราทำการ Migrate ASP.NET ไปยัง IIS Server เครื่องอื่น แล้วเกิด Error Unable Session State Request เนื่องจากไม่ได้ทำการ Enable Service ที่ชื่อ ASP.NET Start State ทำให้ไม่สามารถรัน ASP.NET บน IIS ได้
{% endhint %}

![](https://codeinsane.files.wordpress.com/2021/02/iis-01.png)

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจากไม่ได้ทำการ Enable Service ที่ชื่อ ASP.NET Start State ซึ่งต้องทำการ Enable Service ก่อน ถึงจะสามารถรัน ASP.NET ได้ตามปกติ
{% endhint %}

## **Configuration**

* ทำการเปิด Services แล้ว Enable Service ที่ชื่อ ASP.NET Start State

![](https://codeinsane.files.wordpress.com/2021/02/iis-02.png)

**อ่านเพิ่มเติม** : [http://bit.ly/3bgWU5y](http://bit.ly/3bgWU5y)
