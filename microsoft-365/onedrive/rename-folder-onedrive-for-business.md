# 📂 Rename Folder OneDrive for Business

{% hint style="info" %}
ในกรณีที่เราใช้งาน OneDrive for Business บน Windows 10 แล้วทำการ Login ผ่าน OneDrive for PC เราจะได้ชื่อโฟลเดอร์เป็นชื่อองค์กร ซึ่งถ้ามีหลายคนใช้งานคอมพิวเตอร์เครื่องเดียวกัน เราจะไม่สามารถแยกได้ว่าโฟลเดอร์ไหนเป็นของเรา
{% endhint %}

{% hint style="success" %}
ผมจะขอยกตัวอย่าง กรณีที่เรามีหลาย Account อย่างผม ซึ่งเป็นทั้งพนักงานและนักศึกษาในสถาบันการศึกษา ก็จะมี 2 Account ซึ่งถ้าทำการ Login ผ่าน OneDrive for PC จะเห็นชื่อโฟลเดอร์ เป็นดังนี้
{% endhint %}

![](https://codeinsane.files.wordpress.com/2021/03/onedrive-01.png?w=636\&h=358)

{% hint style="warning" %}
ใน Registry จะเห็นเป็น Business1 ( STU ) และ Business2 ( NIDA )
{% endhint %}

## **Get Started**

* ทำการ Pause Sync OneDrive

![](https://codeinsane.files.wordpress.com/2021/03/rename-01.png?w=636)

* ทำการ Rename OneDrive Folder

![](https://codeinsane.files.wordpress.com/2021/03/rename-02.png?w=636\&h=358)

* กดปุ่ม Win + R แล้วพิมพ์ regedit

![](https://codeinsane.files.wordpress.com/2021/03/rename-03.png?w=636\&h=335)

* ทำการแก้ไข Path ใน HKEY\_CURRENT\_USER ( HKCU )

```
HKCU\SOFTWARE\Microsoft\OneDrive\Accounts\Business1\UserFolder
```

```
HKCU\SOFTWARE\Microsoft\OneDrive\Accounts\Business1\ScopeIdToMountPointPathCache\ID
```

```
HKCU\SOFTWARE\Microsoft\OneDrive\Accounts\Business1\Tenants\name\path
```

```
HKCU\SOFTWARE\SyncEngines\Providers\OneDrive\ID\MountPoint
```

* ทำการแก้ไข Path ใน HKEY\_LOCAL\_MACHINE ( HKCM )

```
HKCM\SOFTWARE\Microsoft\Security Center\Provider\CBP\ID\NAMESPACE
```

{% code overflow="wrap" %}
```
HKCM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\SyncRootManager\ID\UserSyncRoots\ID
```
{% endcode %}

* เข้าไปที่ Path ในไฟล์

```
%UserProfile%\AppData\Local\Microsoft\OneDrive\settings\Business1\ID.ini
```

* ทำการ Resume Sync OneDrive

![](https://codeinsane.files.wordpress.com/2021/03/rename-04.png?w=636)

* จะแสดง Folder ที่เราสามารแยกได้แล้วว่าเป็นของ Account ไหน

![](https://codeinsane.files.wordpress.com/2021/03/rename-05.png?w=636\&h=358)

**อ่านเพิ่มเติม** : [http://bit.ly/3kVkDfZ](http://bit.ly/3kVkDfZ)
