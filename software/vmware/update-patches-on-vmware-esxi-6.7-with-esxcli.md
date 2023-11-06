# 🌠 Update Patches on VMware ESXi 6.7 with ESXCLI

{% hint style="info" %}
โดยปกติการ Update Patches จะแบ่งตามระดับความรุนแรง ( Severity ) ของ Vulnerable เราอาจเลือก Update Patches เฉพาะที่เป็นช่องโหว่ร้ายแรง ( Critical ) ซึ่งเราสามารถดูได้จาก [CVE Detail](https://www.cvedetails.com/) โดยจะบอกถึงรายละเอียดของช่องโหว่ รวมถึง Risk Score ซึ่งบน VMware สามารถทำการ Update Patches ได้ 2 วิธี คือ 1. ผ่านทาง Command Line จะเหมาะกับกรณีที่ Host ไม่เยอะ 2. ผ่านทาง VMware vSphere Update Manager จะเหมาะกับกรณีที่ Host เยอะ
{% endhint %}

## **Get Started**

* ทำการดาวน์โหลด Patch ผ่านทาง [VMware Patch Portal](https://my.vmware.com/group/vmware/patch#search)

![](https://codeinsane.files.wordpress.com/2020/09/patch-01-2.png)

* ทำการ Upload ไปยัง Datastore ของ VMware ESXi

![](https://codeinsane.files.wordpress.com/2020/09/patch-02.png)

* ทำการ Enable SSH

![](https://codeinsane.files.wordpress.com/2020/09/patch-03.png)

* ทำการ Update Patches

<pre data-title="#" data-overflow="wrap"><code><strong>esxcli software vib update -d "/vmfs/volumes/datastore/patch/PatchName.zip"
</strong></code></pre>

{% code overflow="wrap" %}
```
Installation Result
Message: The update completed successfully, but the system needs to be rebooted for the changes to be effective.
Reboot Required: true
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3mhgKCd](https://bit.ly/3mhgKCd)
