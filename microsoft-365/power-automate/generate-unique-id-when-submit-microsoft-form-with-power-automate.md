# 🤖 Generate Unique ID when Submit Microsoft Form with Power Automate

{% hint style="info" %}
ในกรณีที่เราทำการ Submit Microsoft Form เราจะได้เลข Responder Id เริ่มตั้งแต่เลข 1 เป็นต้นไป ซึ่งถ้าเราทำเป็น Digital Form แล้วมันจะดูไม่ Professional เท่าไหร่ เราสามาร Custom ID ให้เป็นรูปแบบที่เราต้องการได้ ซึ่งผมจะใช้ 5 ตัวอักษร โดยใช้ปีขึ้นก่อน เช่น 65001
{% endhint %}

## **Get Started**

* เข้าไปที่หน้าเว็บ [https://asia.flow.microsoft.com/en-us/](https://asia.flow.microsoft.com/en-us/)

<figure><img src="../../.gitbook/assets/flow-01 (1).png" alt=""><figcaption></figcaption></figure>

* คลิก My flows แล้วเลือก New Automated from blank

<figure><img src="../../.gitbook/assets/flow-02 (1).png" alt=""><figcaption></figcaption></figure>

* ทำการกำหนด Flow name และเลือก When a new response is submitted แล้วคลิก Create <mark style="color:red;">คำเตือนชื่อต้องมากกว่า 3 ตัวขึ้นไป</mark>

<figure><img src="../../.gitbook/assets/uniqueid-01.png" alt=""><figcaption></figcaption></figure>

* เลือก Form Id แล้วคลิก Next step

<figure><img src="../../.gitbook/assets/uniqueid-02.png" alt=""><figcaption></figcaption></figure>

* เลือก Get response details ทำการกรอก Form Id และ Response Id แล้วคลิก Next step

<figure><img src="../../.gitbook/assets/uniqueid-03.png" alt=""><figcaption></figcaption></figure>

* เลือก Initialize variable ตั้งชื่อ varGenerateID กำหนด Type เป็น String

<figure><img src="../../.gitbook/assets/uniqueid-04.png" alt=""><figcaption></figcaption></figure>

* ทำการระบุ Expression แล้วคลิก Next step

{% code overflow="wrap" %}
```
add(mul(int(formatDateTime(outputs('Get_response_details')?['body/submitDate'],'yy', 'th-SE')), 1000), triggerOutputs()?['body/resourceData/responseId'])
```
{% endcode %}

* เลือก Create item แล้วทำการกรอกค่าที่รับมาจาก Microsoft Form เพื่อลง SharePoint List โดยตรง Title เลือกเป็น varGenerateID

<figure><img src="../../.gitbook/assets/uniqueid-05.png" alt=""><figcaption></figcaption></figure>
