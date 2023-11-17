# 🧿 Install Docker on Windows Subsystem for Linux

{% hint style="info" %}
หลังจากที่ได้ลองติดตั้ง Web Server บน Windows Subsystem for Linux ( WSL ) กันไปแล้ว เราจะมาลองติดตั้ง Docker บน WSL เพื่อทำการสร้าง Container กันบ้าง
{% endhint %}

## **Requirement**

* Enable Window Subsystem for Linux ( WSL )
* Install Ubuntu 18.04 LTS from Microsoft Store
* Install Docker Desktop for Windows

## **Install**

* ทำการ Update และ Upgrade

{% code title="#" %}
```
apt-get update && apt-get upgrade -y
```
{% endcode %}

* ทำการติดตั้ง Package

{% code title="#" overflow="wrap" %}
```
apt-get install apt-transport-https ca-certificates curl software-properties-common -y
```
{% endcode %}

* ทำการเพิ่ม Docker Public Key

{% code title="#" %}
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
{% endcode %}

* ทำการตรวจสอบ Fingerprint จาก 8 ตัวสุดท้าย

{% code title="#" %}
```
apt-key fingerprint 0EBFCD88
```
{% endcode %}

```
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

* ทำการเพิ่ม Stable Repository

{% code title="#" overflow="wrap" %}
```
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
{% endcode %}

* ทำการติดตั้ง Docker CE

{% code title="#" %}
```
apt-get install docker-ce -y
```
{% endcode %}

* ทำการระบุ Docker Host เพื่อทำการ Connect ผ่าน Daemon Socket

{% code title="#" %}
```
docker -H localhost:2375 images
```
{% endcode %}

* ทำการกำหนด Environment Variable

{% code title="#" %}
```
export DOCKER_HOST=localhost:2375
```
{% endcode %}

{% code title="#" %}
```
echo "export DOCKER_HOST=localhost:2375" >> ~/.bash_profile
```
{% endcode %}

* เปิดโปรแกรม Docker Desktop เลือก General แล้วคลิก Expose daemon

![Docker-01.png](../../.gitbook/assets/docker-01.png)

**อ่านเพิ่มเติม** : [https://dockr.ly/2rgbOBK](https://dockr.ly/2rgbOBK), [https://bit.ly/2oT6kPV](https://bit.ly/2oT6kPV)
