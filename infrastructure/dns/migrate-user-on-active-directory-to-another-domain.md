# 📬 Migrate User on Active Directory to Another Domain

{% hint style="info" %}
การ Migrate User บน Active Directory จาก Domain เดิมไปยัง Domain อื่น จะไม่เหมือนการ Export & Import ที่อยู่บน Domain เดียวกัน แต่จะต้องทำการเปลี่ยน DN ให้เป็น Domain ตัวใหม่ และต้องทำการสร้าง OU รอไว้ ก่อนที่จะทำการสร้าง User Object
{% endhint %}

## **Get Started**

* ทำการ Export Organization Unit ( OU ) เฉพาะ OU ที่อยู่ใน HQ โดยใช้ dsquery

{% code title="C:\>" %}
```
dsquery ou "OU=HQ,DC=domain,DC=local" > c:\csv\list_ou_hq.txt
```
{% endcode %}

* ทำการเปลี่ยน **domain.local** เป็น **lab.local**

```
"OU=HQ,DC=lab,DC=local"
"OU=AC,OU=HQ,DC=lab,DC=local"
"OU=IT,OU=HQ,DC=lab,DC=local"
"OU=PR,OU=HQ,DC=lab,DC=local"
"OU=PO,OU=HQ,DC=lab,DC=local"
```

* ทำการ Import Organization Unit ( OU ) จากไฟล์ **list\_ou\_hq.txt**

{% code title="C:\>" %}
```
for /F %i in (c:\csv\list_ou_hq.txt) do dsadd ou %i
```
{% endcode %}

* ทำการตรวจสอบ Organization Unit ( OU ) ผ่านทาง Powershell ถ้าไม่ครบให้ทำการ Import OU ให้ครบก่อนทำการ Import User

{% code title="PS:\>" overflow="wrap" %}
```
(Get-ADOrganizationalUnit -Filter * -SearchBase 'OU=HQ,DC=domain,DC=local' | Select Name).count
```
{% endcode %}

* ทำการ Export Users ที่อยู่ใน _OU=HQ_ โดยใช้ CSVDE

{% code title="C:\>" overflow="wrap" %}
```
csvde -r "(objectclass=user)" ^
 -d "OU=HQ,DC=domain,DC=local" ^
 -f c:\csv\all_users.csv ^
 -l "DN, objectClass, ou, distinguishedName, name, cn, sn, givenName, displayName, sAMAccountName, userPrincipalName"
```
{% endcode %}

* ทำการเปลี่ยน **domain.local** เป็น **lab.local** ใน Column DN

```
"CN=Adam Smith,OU=AC,OU=HQ,DC=lab,DC=local"
"CN=Alan Turing,OU=IT,OU=HQ,DC=lab,DC=local"
"CN=Elizabeth Olsen,OU=PR,OU=HQ,DC=lab,DC=local" 
"CN=Jack Ma,OU=PO,OU=HQ,DC=lab,DC=local"
```

* ทำการ Import Users จากไฟล์ _all\_users.csv_

{% code title="C:\>" %}
```
csvde -i -k -f c:\csv\all_users.csv
```
{% endcode %}

* ทำการตรวจสอบ Users ผ่านทาง Powershell

{% code title="PS:\>" %}
```
(Get-ADUser -Filter * -SearchBase 'OU=HQ,DC=domain,DC=local').count
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2MFPjTf](https://bit.ly/2MFPjTf), [https://bit.ly/31ocxBE](https://bit.ly/31ocxBE)
