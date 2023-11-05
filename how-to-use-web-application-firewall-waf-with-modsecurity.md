# How to use Web Application Firewall (WAF) with ModSecurity

{% hint style="info" %}
ModSecurity เป็น Module Security ของ Apache ที่ใช้ในการป้องการโจมตี ทำหน้าที่เป็นเหมือน Web Application Firewall (WAF) ซึ่งบริการนี้ที่เรารู้จักกันดีก็คือ Cloudflare WAF แต่วันนี้เราจะมาลองเล่น ModSecurity ของ Apache กัน
{% endhint %}

## **Get Started**

* ทำการ Update และ Upgrade

```
apt-get update && apt-get upgrade -y
```

* ทำการติดตั้ง Package

```
apt-get install libapache2-mod-security2 -y
```

* ทำการ Enable Module

```
a2enmod security2
```

* ทำการ Restart Apache

```
systemctl restart apache2
```

* ทำการ Check Module

```
apachectl -M | grep security
---
 security2_module (shared)
```

* ทำการกำหนด Config

```
cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```

* ทำการแก้ไขไฟล์ `/etc/modsecurity/modsecurity.conf`

```
vi /etc/modsecurity/modsecurity.conf
---
SecRuleEngine On
```

* ทำการติดตั้ง Core Rule Set

{% code fullWidth="false" %}
```
git clone https://github.com/coreruleset/coreruleset.git && cd coreruleset
```
{% endcode %}

* ทำการ Copy Core Rule Set

{% code overflow="wrap" %}
```
cp crs-setup.conf.example /etc/modsecurity/crs-setup.conf && cp -r rules/ /etc/modsecurity/
```
{% endcode %}

* ทำการแก้ไขไฟล์ /etc/apache2/mods-enabled/security2.conf

```
vi /etc/apache2/mods-enabled/security2.conf
---
<IfModule security2_module>
        # Default Debian dir for modsecurity's persistent data
        SecDataDir /var/cache/modsecurity

        # Include all the *.conf files in /etc/modsecurity.
        # Keeping your local configuration in that directory
        # will allow for an easy upgrade of THIS file and
        # make your life easier
        IncludeOptional /etc/modsecurity/*.conf
        Include /etc/modsecurity/rules/*.conf

        # Include OWASP ModSecurity CRS rules if installed
        #IncludeOptional /usr/share/modsecurity-crs/*.load
</IfModule>
```

* ทำการ Restart Apache

```
systemctl restart apache2
```

**อ่านเพิ่มเติม** : [https://bit.ly/3ERILe5](https://bit.ly/3ERILe5)
