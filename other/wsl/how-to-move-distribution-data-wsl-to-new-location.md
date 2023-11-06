# 🧿 How to move Distribution Data WSL to new Location

{% hint style="info" %}
หลังจากที่ได้มีการแบ่ง Partition บน Windows ออกเป็น 2 Partition ระหว่างเก็บไฟล์เอกสารพวก Document กับเก็บพวก Code และ Project เลยคิดว่า ควรจะย้าย Distribution Data WSL มาไว้ด้วยกันซะเลย เพราะมันก็อยู่ใน Group เดียวกันเวลาทำงานอยู่แล้ว จะได้ไม่ต้องไปยุ่งกับ Drive C
{% endhint %}

## **Get Started**

* ทำการตรวจสอบ Distribution ทั้งหมด

```
wsl -l -v
```

* ทำการ Export Distribution Data

```
wsl --export docker-desktop docker-desktop.tar
```

* ทำการ Unregister Distribution

```
wsl --unregister docker-desktop
```

* ทำการ Import Data to new Location

```
wsl --import docker-desktop E:\wsl\docker-desktop docker-desktop.tar --version 2
```

**อ่านเพิ่มเติม** : [https://bit.ly/3QkGFJ7](https://bit.ly/3QkGFJ7)
