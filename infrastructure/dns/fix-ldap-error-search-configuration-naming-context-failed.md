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

{% code title="C:\>" %}
```
ntdsutil
```
{% endcode %}

* ทำการพิมพ์ ldap policies

{% code title="ntdsutil:" %}
```
ldap policies
```
{% endcode %}

* ทำการพิมพ์ connections

{% code title="ldap policy:" %}
```
connections
```
{% endcode %}

* ทำการพิมพ์ Connect to server localhost

```
server connections: Connect to server localhost
Binding to localhost ...
Connected to localhost using credentials of locally logged on user.
```

* ทำการ Exit Connection

{% code title="server connections:" %}
```
q
```
{% endcode %}

* ลองทำการ Show Values

{% code title="ldap policy:" %}
```
Show Values
```
{% endcode %}

```
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

{% code title="ldap policy:" %}
```
set Maxpagesize to 50000
```
{% endcode %}

* ทำการ Commit

{% code title="ldap policy:" %}
```
commit Changes
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3CxE3kw](https://bit.ly/3CxE3kw)
