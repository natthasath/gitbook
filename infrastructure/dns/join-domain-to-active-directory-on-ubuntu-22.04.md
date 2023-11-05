# 📬 Join Domain to Active Directory on Ubuntu 22.04

{% hint style="info" %}
หลายคนคงเคย Join Domain กับ Active Directory บน Windows กันมาบ้างแล้ว แต่เราจะมาลอง Join Domain กับ Active Directory บน Ubuntu กันบ้าง ซึ่งหลักการก็จะคล้าย ๆ กับการ Join Domain บน Windows ถ้าเราเข้าใจ Concept
{% endhint %}

## **Get Started**

* ทำการ Update และ Upgrade

```
apt-get update && apt-get upgrade -y
```

* ทำการติดตั้ง Package

{% code overflow="wrap" %}
```
apt-get install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin krb5-user -y
```
{% endcode %}

* ทำการกำหนด Hostname

<pre><code><strong>hostnamectl set-hostname ubt.lab.local
</strong></code></pre>

* ทำการตรวจสอบ Hostname

```
hostnamectl
---
Static hostname: ubt.lab.local
       Icon name: computer-vm
         Chassis: vm
      Machine ID: 4409f54e40fc472586aca1ba7aa9772b
         Boot ID: 181d32c358b14680adef878986c247a5
  Virtualization: vmware
Operating System: Ubuntu 22.04.1 LTS
          Kernel: Linux 5.15.0-53-generic
    Architecture: x86-64
 Hardware Vendor: VMware, Inc.
  Hardware Model: VMware Virtual Platform
```

* ทำการแก้ไขไฟล์ /etc/krb5.conf

<pre><code>vi /etc/krb5.conf
---
[libdefaults]
<strong>        default_realm = LAB.LOCAL
</strong>
[realms]
<strong>        LAB.LOCAL = {
</strong><strong>                kdc = dc1.lab.local
</strong><strong>                kdc = dc2.lab.local
</strong><strong>                admin_server = dc1.lab.local
</strong><strong>                default_domain = lab.local
</strong>        }
</code></pre>

* ทำการ Discover Domain

<pre><code><strong>realm discover lab.local
</strong></code></pre>

* ทำการ Join Domain

<pre><code><strong>realm join --user=Administrator lab.local
</strong></code></pre>

* ทำการ Verify Domain

```
realm list
---
lab.local
  type: kerberos
  realm-name: LAB.LOCAL
  domain-name: lab.local
  configured: kerberos-member
  server-software: active-directory
  client-software: sssd
  required-package: sssd-tools
  required-package: sssd
  required-package: libnss-sss
  required-package: libpam-sss
  required-package: adcli
  required-package: samba-common-bin
  login-formats: %U@lab.local
  login-policy: allow-realm-logins
```

**อ่านเพิ่มเติม** : [https://bit.ly/43KCQTo](https://bit.ly/43KCQTo)
