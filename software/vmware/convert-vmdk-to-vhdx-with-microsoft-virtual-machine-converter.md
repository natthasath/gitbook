# 🌠 Convert VMDK to VHDX with Microsoft Virtual Machine Converter

{% hint style="info" %}
หลังจากที่ได้ลองเล่น Hyper-V ก็รู้สึกติดใจ Interface ในการใช้งาน และด้วยความเป็น Software ที่ติดมากับ Microsoft ทำให้การใช้งานระหว่างเครื่อง Host กับ VM ไม่จำเป็นต้องลง VMware Tools เหมือนการใช้งานบน VMware Workstation แถมมี Software ที่ช่วยในการ Convert จาก VMDK มาเป็น VHDX ด้วย Microsoft Virtual Machine Converter ( MVMC )
{% endhint %}

## **Support Virtual Machine**

{% hint style="warning" %}
ข้อควรระวังในการใช้งาน MVMC คือการ [Support Virtual Machine](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn873998\(v=ws.11\)) ขึ้นอยู่กับ Version ของ MVMC ซึ่งจะไม่ Support Virtual Machine รุ่นใหม่ ๆ เท่าไหร่ เช่น MVMC 3.0 จะไม่ Support พวก Windows 10, Windows Server 2016 ส่วน OS อื่น ๆ นอกเหนือจาก Windows ก็ Support เช่นกัน ไม่ว่าจะเป็น VMware, Ubuntu, CentOS, Debian, Oracle Linux
{% endhint %}

## **Download**

* [Microsoft Virtual Machine Converter 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=42497)

## **Get Started**

* ทำการ Import Module ใน Powershell คลิกขวา Run as Administrator

{% code title="PS C:\>" %}
```
Import-Module 'C:\Program Files\Microsoft Virtual Machine Converter\MvmcCmdlet.psd1'
```
{% endcode %}

* &#x20;ทำการ Convert VMDK to VHDX

{% code title="PS C:\>" %}
```
ConvertTo-MvmcVirtualHardDisk ^
 -SourceLiteralPath d:\scratch\vmx\VM-disk1.vmdk ^
 -VhdType DynamicHardDisk ^
 -VhdFormat vhdx ^
 -destination c:\vm-disk1
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2MhWwoB](https://bit.ly/2MhWwoB)
