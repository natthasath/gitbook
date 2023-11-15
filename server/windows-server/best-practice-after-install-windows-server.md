# 👺 Best Practice After Install Windows Server

{% hint style="info" %}
ในกรณีที่เราทำการ Install Windows Server เสร็จเรียบร้อย เราจะต้องทำการ Config & Enable Service รวมถึงการติดตั้ง Tool & Software ที่ต้องการใช้งานต่าง ๆ ซึ่งผมได้ทำการรวบรวมสิ่งที่ต้องทำ รวมถึง List Software พื้นฐานที่ต้องทำการติดตั้ง เพื่อเป็นมาตรฐานในการติดตั้ง Windows Server
{% endhint %}

**Download**

* [Script Windows Powershell](https://github.com/natthasath/script/blob/main/powershell-script/windows/After-Install.ps1)

**Config & Enable Service**

* Install VMware Tools ( VMXNET3 )
* Setting Computer Name
* Setting IP Address ( IPv4 )
* Setting Region ( United States )
* Setting Time Zone ( SE Asia Standard Time )
* Setting Short Date ( d/M/yyyy )
* Setting Short Time ( H:mm )
* Setting Long Date ( dddd, MMMM d, yyyy )
* Setting Long Time ( H:mm:ss )
* Setting Language ( EN, TH )
* Enable Remote Desktop ( 3389 )
* Enable Firewall ICMP
* Enable Firewall SMTP
* Disable Windows Update
* Join Domain
* Restart Computer

**List Software**

* Microsoft Edge
* Visual Studio Code
* ESET NOD32
* Git

**Option Software**

* AOMEI Partition Assistant
* Apache Jmeter
* Dataedo
* Ngrok
* Postman
* Putty
* Redis GUI
* SourceTree Enterprise
* WindowTop
* WinRAR
* WinSCP
* Zoomit
