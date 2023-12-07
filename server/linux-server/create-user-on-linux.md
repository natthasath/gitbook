# 👿 Create User on Linux

{% hint style="info" %}
โดยปกติการสร้าง User บน Linux จะไม่ได้สร้าง Home Directory รวมถึง Assign Group มาให้ในค่า Default ซึ่งเราจะต้องมาทำในภายหลัง
{% endhint %}

## Get Started

* ทำการ Create User

{% code title="#" %}
```
useradd -m -s /bin/bash -u 1234 devops
```
{% endcode %}

* ทำการ Set Password

{% code title="#" %}
```
passwd devops
```
{% endcode %}

```
New password:
Retype new password:
passwd: password updated successfully
```

* ทำการตรวจสอบ Home Directory

{% code title="#" %}
```
ls -la /home/devops/
```
{% endcode %}

```
drwxr-x--- 2 devops devops 4096 Dec  7 06:24 .
drwxr-xr-x 4 root   root   4096 Dec  7 06:24 ..
-rw-r--r-- 1 devops devops  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 devops devops 3771 Jan  6  2022 .bashrc
-rw-r--r-- 1 devops devops  807 Jan  6  2022 .profile
```

* ทำการ Add User to Group

{% code title="#" %}
```
usermod -a -G adm,cdrom,sudo,dip,plugdev,lxd devops
```
{% endcode %}

* ทำการตรวจสอบ User Group

{% code title="#" %}
```
id devops
```
{% endcode %}

{% code overflow="wrap" %}
```
uid=1234(devops) gid=1234(devops) groups=1234(devops),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
```
{% endcode %}
