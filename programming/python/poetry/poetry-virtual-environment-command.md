# 🐍 Poetry Virtual Environment Command

{% hint style="info" %}
หากใครเคยลองใช้ Virtualenv ที่เป็น Standard Library ของภาษา Python สำหรับสร้าง Virtual Environment ของแต่ละ Project แยกออกจากกัน ทำให้แต่ละ Project ที่ใช้ Library เดียวกันแต่คนละ Version ไม่ Conflict กันนั่นเอง แต่ผมจะขอแนะนำเครื่องมืออีกตัวที่ชื่อว่า Poetry เนื่องจากมันสามารถจัดการกับ Dependency Management, Dependency Lock File ได้
{% endhint %}

## **Poetry Command**

* Poetry Version

```
poetry --version
```

* Poetry Initial

```
poetry init
```

* Poetry Install

```
poetry install
```

* Poetry Update

```
poetry update
```

* Poetry Add Package

```
poetry add requests
```

* Poetry Remove Package

```
poetry remove requests
```

* Poetry List Package

```
poetry show
```

* Poetry Run

```
poetry run
```

* Poetry Export Package to File

```
poetry export --without-hashes --without-urls | awk '{ print $1 }' FS=';' > requirements.txt
```

**อ่านเพิ่มเติม** : [https://bit.ly/45LMZz7](https://bit.ly/45LMZz7)
