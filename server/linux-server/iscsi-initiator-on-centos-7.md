# 👿 iSCSI Initiator on CentOS 7

{% hint style="info" %}
หลังจากที่ลองต่อ iSCSI บน Windows และ Linux กันไปแล้ว เราจะมาลองต่อ iSCSI บน CentOS ซึ่งการติดตั้งก็จะคล้าย ๆ กัน แต่หลังจากที่ต่อ iSCSI ได้แล้ว หากต้องการจะ Mount Volume บน CentOS จะไม่ได้ใช้ LVM แต่จะใช้ ZFS แทน ซึ่งจะเขียนในบทความต่อไป
{% endhint %}

## **Get Started**

* ทำการ Update และ Upgrade

{% code title="#" %}
```
yum update && yum upgrade -y
```
{% endcode %}

* ทำการติดตั้ง Package

{% code title="#" %}
```
yum install iscsi-initiator-utils -y
```
{% endcode %}

* แก้ไขไฟล์ /etc/iscsi/iscsid.conf

{% code title="#" %}
```
vi /etc/iscsi/iscsid.conf
```
{% endcode %}

```
node.startup = automatic
```

* ตรวจสอบ Target ของ Storage โดย Default Port เป็น 3260

{% code title="#" %}
```
iscsiadm -m discovery -t st -p 1.1.1.2
```
{% endcode %}

```
10.10.10.2:3260,1 iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync
1.1.1.2:3260,1 iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync
```

* หากกำหนด Authentication ไว้

{% code title="#" %}
```
vi /etc/iscsi/iscsid.conf
```
{% endcode %}

```
node.session.auth.username = username
node.session.auth.password = password
```

* ทำการ Login

{% code title="#" %}
```
iscsiadm -m node -l -T iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync -p 1.1.1.2
```
{% endcode %}

```
Logging in to [iface: default, target: iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync, portal: 1.1.1.2,3260] (multiple)
Login to [iface: default, target: iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync, portal: 1.1.1.2,3260] successful.
```

* ในกรณีที่ไม่ต้อง Connect แล้ว ให้ทำการ Logout

{% code title="#" %}
```
iscsiadm -m node -u
```
{% endcode %}

* ตรวจสอบ New Disk จาก Log ที่อยู่บน Kernel Messages

{% code title="#" %}
```
dmesg | grep sd
```
{% endcode %}

```
[ 9311.769734] sd 54:0:0:0: Attached scsi generic sg2 type 0
[ 9311.769879] sd 54:0:0:0: [sdb] 104857600 512-byte logical blocks: (53.7 GB/50.0 GiB)
[ 9311.771863] sd 54:0:0:0: [sdb] Write Protect is off
[ 9311.771872] sd 54:0:0:0: [sdb] Mode Sense: 43 00 00 08
[ 9311.772251] sd 54:0:0:0: [sdb] Write cache: disabled, read cache: enabled, doesn't support DPO or FUA
[ 9311.777438] sd 54:0:0:0: [sdb] Attached SCSI disk
```

* ตรวจสอบ New Disk จากการ Scan

{% code title="#" %}
```
fdisk -l
```
{% endcode %}

```
Disk /dev/sdb: 50 GiB, 53687091200 bytes, 104857600 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 8388608 bytes
```

* ตรวจสอบ Connection ที่ต่อ iSCSI อยู่

{% code title="#" %}
```
iscsiadm -m session
```
{% endcode %}

```
tcp: [52] 1.1.1.2:3260,1 iqn.2004-08.jp.buffalo.8857eeb78f4f.rsync (non-flash)
```
