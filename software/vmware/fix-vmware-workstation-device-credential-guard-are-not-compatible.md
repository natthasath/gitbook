# 🌠 Fix VMware Workstation Device / Credential Guard are not Compatible

{% hint style="info" %}
การใช้งาน VMware Workstation กับ Hyper-V ดูจะไม่สามารถใช้งานทั้ง 2 ตัวพร้อมกันได้ ซึ่งถ้าหากทำการ Enable Hyper-V ก็จะไม่สามารถใช้งาน VMware Workstation ได้ รวมถึง Virtual Box ด้วย โดยส่วนตัวผมเริ่มชอบ Hyper-V มากกว่า VMware Workstation แต่ก็ต้องใช้มันอยู่ ก็จะเกิดอาการที่เรียกว่า _**รักพี่เสียดายน้อง**_
{% endhint %}

![Fix-01.png](<../../.gitbook/assets/fix-01 (1).png>)

{% hint style="danger" %}
**Cause** :สาเหตุเนื่องมาจาก Virtualization Application ขึ้นอยู่กับ Hardware Virtualization เช่น Intel VT-X หรือ AMD-V ซึ่งการใช้งานไม่สามารถ Share ร่วมกันได้ ทำให้ต้องเลือกใช้งาน Virtualization Application ตัวใดตัวหนึ่งเท่านั้น
{% endhint %}

## **Configuration**

* ทำการ Disable Hyper-V

{% code title="#" %}
```
bcdedit /set hypervisorlaunchtype off
```
{% endcode %}

* &#x20;ทำการ Enable Hyper-V

{% code title="#" %}
```
bcdedit /set hypervisorlaunchtype auto
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/2Gs3JTb](https://bit.ly/2Gs3JTb)
