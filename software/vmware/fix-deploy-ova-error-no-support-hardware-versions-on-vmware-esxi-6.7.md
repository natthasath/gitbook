# 🌠 Fix Deploy OVA Error no Support Hardware Versions on VMware ESXi 6.7

{% hint style="info" %}
ในกรณีที่เราทำการ Deploy OVF Template ที่มี Format แบบ OVA แล้ว Virtual Hardware Version ไม่ Compatible กับ VMware ESXi Version จะทำให้ไม่สามารถ Deploy ได้ สามารถตรวจสอบ Virtual Hardware Compatible ได้ที่ [http://bit.ly/3U2dEBN](http://bit.ly/3U2dEBN)
{% endhint %}

<figure><img src="../../.gitbook/assets/virtualhw-01.png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
**Cause** :สาเหตุเนื่องมาจาก Virtual Hardware Version ของไฟล์ OVA ไม่ Compatible กับ VMware ESXi Version แต่เราสามารแก้ไข Virtual Hardware Version ของไฟล์ VMX ให้ตรงกับ VMware ESXi Version ที่รองรับ ก่อนทำการ Convert เป็นไฟล์ OVA
{% endhint %}

## **Configuration**

* ทำการแก้ไขไฟล์ vm.vmx

```
virtualHW.version = "14"
```

* ทำการแก้ไขค่า SVGA Ram Size ไม่ให้เกิน 128 MB

```
svga.vramSize = "134217728"
vmotion.checkpointSVGAPrimarySize = "134217728"
```

**อ่านเพิ่มเติม** : [bit.ly/3GEQ1fq](http://bit.ly/3GEQ1fq), [http://bit.ly/3XEYVzQ](http://bit.ly/3XEYVzQ)
