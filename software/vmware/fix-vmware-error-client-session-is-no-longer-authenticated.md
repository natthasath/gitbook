# 🌠 Fix VMware Error Client Session is no Longer Authenticated

{% hint style="info" %}
ในกรณีที่เราทำการ Login เข้าใช้งาน VMware vCenter แล้วไม่สามารถทำการ Login ได้ ซึ่งจะถูกบังคับให้ทำการ Login ใหม่ ถึงแม้จะทำการ Reinstall Enhanced Authentication Plugin หรือแม้แต่ทำการ Disable Plugin ทั้งหมดแล้วก็ตาม แต่พอลองทำการ Login ด้วย Browser อื่น หรือ ทำการ Login บน Incognito Mode ก็สามารถทำการ Login ได้ปกติ
{% endhint %}

![vSphere-01](../../.gitbook/assets/vsphere-01.png)

{% hint style="danger" %}
**Cause** : สาเหตุยังไม่ทราบแน่ชัด ได้ลองทำการค้นหาแล้วแต่ยังไม่สามารถระบุสาเหตุได้ว่าเกิดจากอะไร ซึ่งสาเหตุนี้อาจเกิดได้ทั้ง Google Chrome และ Firefox แต่ยังมีวิธีแก้ ที่สามารถทำได้อย่างปลอดภัย โดยการ Clear Data พวก Cookie and Site Data บน Web Browser
{% endhint %}

## **Configuration**

* เปิดโปรแกรม Firefox แล้วคลิก Open Menu -> Options -> Privacy & Security -> Clear Data

![vSphere-02.png](../../.gitbook/assets/vsphere-02.png)

* เลือก Cookies and Site Data และ Cached Web Content แล้วคลิก Clear

![vSphere-03.png](../../.gitbook/assets/vsphere-03.png)
