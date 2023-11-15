# 📙 Fix Unified Group is not Recognized on Powershell

{% hint style="info" %}
ในกรณีที่เราทำการ Delete SharePoint Site ผ่าน Powershell เราจะต้องทำการ Delete Group ของ SharePoint Site ออกก่อน ซึ่งจะต้องใช้คำสั่ง Unified Group แต่เราจะไม่สามารถทำผ่าน Module  ของ Azure AD Powershell ได้
{% endhint %}

{% hint style="danger" %}
**Cause** : สาเหตุเนื่องมาจากคำสั่ง Unified Group จะต้องรันใน Exchange Online Powershell แทน Azure AD Powershell ซึ่งมีวิธีแก้ 2 วิธี คือ 1. ทำการ Install Module ของ Exchange Online 2. ทำการสร้าง Session ต่อไปยัง Exchange Online
{% endhint %}

## **Configuration**

### Solution 1&#x20;

* ทำการ Install Module

{% code title="PS C:\>" %}
```
Install-Module -Name ExchangeOnlineManagement
```
{% endcode %}

* ทำการ Connect Exchange Online

{% code title="PS C:\>" %}
```
Connect-ExchangeOnline -Credential $credential
```
{% endcode %}

### Solution 2&#x20;

* ทำการ Set Execution Policy เป็น RemoteSigned เนื่องจากมีการ Download จาก Internet ซึ่งจะต้องทำ Trust กัน

{% code title="PS C:\>" %}
```
Set-ExecutionPolicy RemoteSigned
```
{% endcode %}

* ทำการ Set WinRM  Authentication เป็นแบบ Basic โดยจะทำการส่งเป็น OAuth Token แทนการส่ง Username และ Password

{% code title="PS C:\>" %}
```
winrm set winrm/config/client/auth @{Basic="true"}
```
{% endcode %}

* ทำการ Connect Exchange Online

{% code title="PS C:\>" %}
```
$username = "username"
```
{% endcode %}

{% code title="PS C:\>" %}
```
$password = "password" | ConvertTo-SecureString
```
{% endcode %}

{% code title="PS C:\>" %}
```
$uri = "https://outlook.office365.com/powershell-liveid/"
```
{% endcode %}

{% code title="PS C:\>" %}
```
$name = "site name"
```
{% endcode %}

{% code title="PS C:\>" overflow="wrap" %}
```
$credential = New-Object System.Management.Automation.PSCredential -ArgumentList $username, $password
```
{% endcode %}

{% code title="PS C:\>" overflow="wrap" %}
```
$session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri $uri -Credential $credential -Authentication Basic -AllowRedirection
```
{% endcode %}

{% code title="PS C:\>" %}
```
Import-PSSession -AllowClobber $session -DisableNameChecking
```
{% endcode %}

{% code title="PS C:\>" overflow="wrap" %}
```
Get-UnifiedGroup -Identity $name | Select-Object DisplayName, EmailAddresses, Notes, ManagedBy, AccessType, PrimarySmtpAddress
```
{% endcode %}

{% code title="PS C:\>" %}
```
Remove-PSSession $session
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2PHBwfg](https://bit.ly/2PHBwfg), [https://bit.ly/3iCgICc](https://bit.ly/3iCgICc)
