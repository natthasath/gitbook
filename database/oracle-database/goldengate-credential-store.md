# 🥥 GoldenGate Credential Store

{% hint style="info" %}
โดยปกติการใช้งาน GGSCI ซึ่งเป็น Command Line ของ GoldenGate จะต้องทำการ Connect Database ด้วย Account ที่มีสิทธิ์เข้าถึง ซึ่งต้องทำการระบุ Username และ Password แต่เราสามารถทำการสร้าง Alias เพื่อให้สามารถ Connect Database ด้วย Credential Store ได้อย่างสะดวกรวดเร็ว
{% endhint %}

## **Get Started**

* ทำการ Connect Database ด้วย GGSCI

{% code title="GGSCI>" %}
```
dblogin userid ggate@ORCL, password ggate
```
{% endcode %}

* ทำการตรวจสอบ Credential Store

{% code title="GGSCI>" %}
```
info credentialstore
```
{% endcode %}

```
ERROR: Unable to open credential store in ./dircrd/.
```

* ทำการสร้าง Credential Store

{% code title="GGSCI>" %}
```
add credentialstore
```
{% endcode %}

```
Credential store created in ./dircrd/.
```

* ทำการสร้าง Alias

{% code title="GGSCI>" %}
```
alter credentialstore add user ggate password ggate alias ggorcl
```
{% endcode %}

```
Credential store in ./dircrd/ altered.
```

* ทำการตรวจสอบ Credential Store อีกครั้งหนึ่ง

{% code title="GGSCI>" %}
```
info credentialstore
```
{% endcode %}

```
Reading from ./dircrd/:

Default domain: OracleGoldenGate

  Alias: ggorcl
  Userid: ggate
```

* ลองทำการ Login GoldenGate ด้วย Alias

{% code title="GGSCI>" %}
```
dblogin useridalias ggorcl
```
{% endcode %}

```
Successfully logged into database.
```

**อ่านเพิ่มเติม** : [https://bit.ly/2vlNkwQ](https://bit.ly/2vlNkwQ), [https://bit.ly/30Ydaml](https://bit.ly/30Ydaml)
