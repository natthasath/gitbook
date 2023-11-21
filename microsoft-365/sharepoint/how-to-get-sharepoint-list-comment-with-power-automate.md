# 📙 How to get SharePoint List Comment with Power Automate

{% hint style="info" %}
หลังจากที่เราทำการเก็บ Approve Comment บน SharePoint List กันไปแล้ว เราจะทำการดึง Comment ที่เราเก็บบน SharePoint List ไปใช้ต่อ เช่น ใช้ในการส่งอีเมล
{% endhint %}

## **Get Started**

* เข้าไปที่หน้าเว็บ [https://asia.flow.microsoft.com/en-us/](https://asia.flow.microsoft.com/en-us/)

<figure><img src="../../.gitbook/assets/flow-01.png" alt=""><figcaption></figcaption></figure>

* คลิก My flows แล้วเลือก New Automated from blank

<figure><img src="../../.gitbook/assets/flow-02.png" alt=""><figcaption></figcaption></figure>

* ทำการกำหนด Flow name และเลือก When an item is created or modified แล้วคลิก Create <mark style="color:red;">คำเตือนชื่อต้องมากกว่า 3 ตัวขึ้นไป</mark>

<figure><img src="../../.gitbook/assets/listcomment-01.png" alt=""><figcaption></figcaption></figure>

* เลือก Form Id แล้วคลิก Next step

<figure><img src="../../.gitbook/assets/listcomment-02.png" alt=""><figcaption></figcaption></figure>

* เลือก Initialize variable สำหรับ Comment ID กำหนด Type เป็น String แล้วคลิก Next step

<figure><img src="../../.gitbook/assets/listcomment-03.png" alt=""><figcaption></figcaption></figure>

* เลือก Initialize variable สำหรับ Comment Text กำหนด Type เป็น String แล้วคลิก Next step

<figure><img src="../../.gitbook/assets/listcomment-04.png" alt=""><figcaption></figcaption></figure>

* เลือก Send an HTTP request to SharePoint ทำการกรอกรายละเอียด แล้วคลิก Next step

```
Uri : _api/web/lists/getbytitle('LIST')/items('ITEMID')/Comments
Headers : accept | application/json;odata=verbose
          content-type | application/json;odata=verbose
```

<figure><img src="../../.gitbook/assets/listcomment-05.png" alt=""><figcaption></figcaption></figure>

* เลือก Compose กำหนด Inputs แล้วคลิก Next Step

```
@{outputs('Send_an_HTTP_request_to_SharePoint')?['body/d/results']}
```

<figure><img src="../../.gitbook/assets/listcomment-06.png" alt=""><figcaption></figcaption></figure>

* เลือก Apply to each กำหนด Outputs ที่ได้จาก Compose แล้วคลิก Add an action

<figure><img src="../../.gitbook/assets/listcomment-07.png" alt=""><figcaption></figcaption></figure>

* เลือก Set variable สำหรับ Comment ID กำหนด Value แล้วคลิก Add an action กรณีที่ต้องการเลือก Comment จะใช้ ID เป็นตัวกำหนด Condition

```
@{items('Apply_to_each')?['ID']}
```

<figure><img src="../../.gitbook/assets/listcomment-08.png" alt=""><figcaption></figcaption></figure>

* เลือก Append to string variable สำหรับ Comment Text กำหนด Value แล้วคลิก Add an action

```
@{items('Apply_to_each')?['Text']}
```

<figure><img src="../../.gitbook/assets/listcomment-09.png" alt=""><figcaption></figcaption></figure>

**อ่านเพิ่มเติม** : [https://bit.ly/3yIoAwS](https://bit.ly/3yIoAwS)
