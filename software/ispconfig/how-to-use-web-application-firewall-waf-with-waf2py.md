# 🌏 How to use Web Application Firewall (WAF) with Waf2Py

{% hint style="info" %}
หลังจากที่เราลง ModSecurity กันไปแล้ว เหมือนจะมีปัญหากับ Virtual Host ทำให้ไม่สามารถใช้งานบน ISPConfig ได้ เราเลยจะมาลองเล่น Waf2Py ของ Nginx + ModSecurity กัน ซึ่งมีหน้าตา User Interface ให้เราได้เข้าไปจัดการได้ง่ายขึ้น ผ่านทาง Web Browser
{% endhint %}

## **Get Started**

* ทำการดาวน์โหลด Waf2Py 1.0

{% code overflow="wrap" %}
```
wget https://github.com/ITSec-Chile/Waf2Py/releases/download/waf2py_1.0/waf2py1.0_bundle.tar.gz
```
{% endcode %}

* ทำการติดตั้ง Waf2Py

{% code overflow="wrap" %}
```
cd Waf2Py/installer/
```
{% endcode %}

```
chmod +x waf2py_installer.sh
```

```
./waf2py_installer.sh
```

* ลองเข้าไปที่ [https://localhost:62443](https://localhost:62443/) แล้วกรอก Username และ Password ด้วย admin : password

<figure><img src="../../.gitbook/assets/waf2py-01.png" alt=""><figcaption></figcaption></figure>

* หลังจาก Login เข้ามาจะเห็นหน้าตาแบบนี้

<figure><img src="../../.gitbook/assets/waf2py-02.png" alt=""><figcaption></figcaption></figure>

* หน้าตา Dashboard

<figure><img src="../../.gitbook/assets/waf2py-03.png" alt=""><figcaption></figcaption></figure>

**อ่านเพิ่มเติม** : [https://bit.ly/3ZPVN5x](https://bit.ly/3ZPVN5x)
