# 🐳 Upgrade Docker Compose

{% hint style="info" %}
ในการใช้งานบาง Docker Compose ผ่าน Compose File โดยมี Format แบบ YAML ที่ใช้ในการ Define Services, Networks และ Volumes จะต้องดู Version ของ Docker Compose หากมีการใช้งาน Docker Swarm จะต้องใช้ Compose File เวอร์ชั่น 3.x ขึ้นไป ซึ่งอาจจะต้องทำการ Upgrade Docker Compose ให้เป็นเวอร์ชั่นล่าสุด
{% endhint %}

## **Get Started**

* ทำการ Uninstall Docker Compose

```
apt-get remove docker-compose
```

```
rm /usr/bin/docker-compose
```

* ทำการค้นหา Latest Version

{% code overflow="wrap" %}
```
VERSION=$(curl --silent https://api.github.com/repos/docker/compose/releases/latest | grep -Po '"tag_name": "\K.*\d')
```
{% endcode %}

* ทำการกำหนด Destination

```
DESTINATION=/usr/bin/docker-compose
```

* ทำการ Download

{% code overflow="wrap" %}
```
curl -L https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m) -o $DESTINATION
```
{% endcode %}

* ทำการกำหนด Permission

```
chmod 755 $DESTINATION
```

**อ่านเพิ่มเติม** : [https://bit.ly/3Th7BtE](https://bit.ly/3Th7BtE)
