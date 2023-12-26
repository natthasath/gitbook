# 🧩 Integrate Microsoft Graph API with Function App on Azure

{% hint style="info" %}
หลังจากที่เราได้ทำการสร้าง Function App กันไปแล้ว คราวนี้ก็ถึงเวลาที่จะต่อกับ Microsoft Graph API โดยมีข้อควรระวังคือไม่ควรคัดลอก JSON มาวาง เพราะอาจจะต้องทำการ Install Extension ซึ่งมันจะไม่ขึ้นให้ Install ต้องทำการ Add Parameter แบบคลิกแทน ถึงจะขึ้นให้ทำการ Install
{% endhint %}

## **Get Started**

* คลิก New Function

![](../../.gitbook/assets/serverless-13.png)

* คลิก HTTP Trigger

![](../../.gitbook/assets/serverless-14.png)

* กำหนดชื่อ Function Name แล้วคลิก Create

![](../../.gitbook/assets/serverless-15.png)

* ทำการแก้ไขไฟล์ run.csx

{% code title="run.csx" %}
```
#r "Newtonsoft.Json"

using System.Net; 
using System.Net.Http; 
using System.Net.Http.Headers;
using Microsoft.Extensions.Logging; 

public static async Task Run(HttpRequestMessage req, string graphToken, ILogger log)
{
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", graphToken);
    return await client.GetAsync("https://graph.microsoft.com/v1.0/me/");
}
```
{% endcode %}

* เลือกฟังก์ชั่นที่เราสร้าง Auth แล้วคลิก Integrate

![](../../.gitbook/assets/serverless-16.png)

* คลิก Inputs

![](../../.gitbook/assets/serverless-17.png)

* เลือก Auth token แล้วคลิก Select

![](../../.gitbook/assets/serverless-18.png)

* ทำการติดตั้ง Extension คลิก Install

![](../../.gitbook/assets/serverless-19.png)

* คลิก Manage App Service Authentication / Authorization

![](../../.gitbook/assets/serverless-20.png)

* ทำการ On App Service Authentication แล้วคลิก Azure Active Directory

![](../../.gitbook/assets/serverless-21.png)

* เลือก Management Mode เป็น Express แล้วคลิก OK

![](../../.gitbook/assets/serverless-22.png)

* เลือก Action Request เป็น Log in with Azure Active Directory แล้วคลิก Save

![](../../.gitbook/assets/serverless-23.png)

* ทำการแก้ไข Resource URL ที่จะยิงไปหา และแก้ไขชื่อ Parameter Name เป็น graphToken แล้วคลิก Save

![](../../.gitbook/assets/serverless-24.png)

* ทำการ Refresh หน้าจอ ฟังก์ชัน Auth จะพร้อมใช้งานแล้ว

![](../../.gitbook/assets/serverless-25.png)

* ลองทำการเรียกผ่าน Browser โดยคลิก Get function URL

![](../../.gitbook/assets/serverless-26.png)

* คลิก Accept

![](../../.gitbook/assets/serverless-27.jpg)

* จะแสดงผลลัพธ์ในรูปแบบ JSON

<figure><img src="../../.gitbook/assets/serverless-28.png" alt=""><figcaption></figcaption></figure>

อ่านเพิ่มเติม : [https://bit.ly/2FSLgi6](https://bit.ly/2FSLgi6)
