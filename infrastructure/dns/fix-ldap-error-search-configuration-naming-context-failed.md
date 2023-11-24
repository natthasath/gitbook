# 📦 Fix Ldap Error Search Configuration Naming Context failed

{% hint style="info" %}
ในกรณีที่เราทำการกำหนดค่า Max Page Size บน Ldap แล้วเกิด Error ในการ Search Configuration Naming Context failed ทำให้ไม่สามารถกำหนดค่า Max Page Size บน Ldap ได้
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจาก อาจเกิดจากติดสิทธิ์ Permission ทำให้ไม่สามารถกำหนดค่า Max Page Size บน Ldap ได้ ซึ่งเราสามารถแก้ไขได้โดยการ Connect โดยใช้ Local Credential
{% endhint %}

{% code overflow="wrap" %}
```
ldap policy: Set MaxPageSize to 5000
*** Error: ldap_search of configurationNamingContext failed with 0x59(89 (Parameter Error).
```
{% endcode %}

## **Configuration**

* ทำการเรียกใช้ NTDS Util Command

```
C:\> ntdsutil
```

* ทำการพิมพ์ ldap policies

```
ntdsutil: ldap policies
```

* ทำการพิมพ์ connections

```
ldap policy: connections
```

* ทำการพิมพ์ Connect to server localhost

```
server connections: Connect to server localhost
Binding to localhost ...
Connected to localhost using credentials of locally logged on user.
```

* ทำการ Exit Connection

```
server connections: q
```

* ลองทำการ Show Values

```
ldap policy: Show Values

Policy                          Current(New)

MaxPoolThreads                  4
MaxPercentDirSyncRequests                       0
MaxDatagramRecv                 4096
MaxReceiveBuffer                        10485760
InitRecvTimeout                 120
MaxConnections                  1000
MaxConnIdleTime                 900
MaxPageSize                     5000
MaxBatchReturnMessages                  0
MaxQueryDuration                        120
MaxTempTableSize                        10000
MaxResultSetSize                        262144
MinResultSets                   0
MaxResultSetsPerConn                    0
MaxNotificationPerConn                  5
MaxValRange                     1500
MaxValRangeTransitive                   0
ThreadMemoryLimit                       0
SystemMemoryLimitPercent                        0
```

* ทำการ Set MaxPageSize

```
ldap policy: set Maxpagesize to 50000
```

* ทำการ Commit

```
ldap policy: commit Changes
```

**อ่านเพิ่มเติม** : [https://bit.ly/3CxE3kw](https://bit.ly/3CxE3kw)
