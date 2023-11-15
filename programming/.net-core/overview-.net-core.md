# 🐹 Overview .NET Core

{% hint style="info" %}
หลายคนคงเคยเรียนภาษา .NET Programming ของทางฝั่ง Microsoft ในวิชาคอมพิวเตอร์กันมาบ้าง ไม่ว่าจะเป็น VB, C# ซึ่งจะยึดติดกับ Platform ของทางฝั่ง Microsoft เอง ต่อมาเมื่อเกิดภาษา Programming ที่เป็น Cross-Platform มากขึ้น Microsoft จึงต้องหันมาทำ .NET Core บ้าง
{% endhint %}

![.NET\_Core-01.png](../../.gitbook/assets/net\_core-01.png)

## Overview

.NET Core เป็น Other Framework ที่ได้รับความนิยมสูงสุดของปี 2019 บน [Stack Overflow](https://insights.stackoverflow.com/survey/2019) จากการที่มันเป็น Programming Language แบบ Cross-Platform นั่นเอง โดยจะใช้ Library แยกจาก .NET Framework แต่จะใช้ Compiler & Runtime Component ร่วมกัน

![.NET\_Core-02.png](../../.gitbook/assets/net\_core-02.png)

เมื่อพัฒนา .NET Core มาซะขนาดนี้ จะให้ใช้ Visual Studio บน Windows มันก็ดูจะเป็น Cross-Platform ที่ใช้ไม่ได้จริง ทาง Microsoft เลยทำ Visual Code ที่เป็น Code Editor แบบ Cross-Platform ขึ้นมารองรับนั่นเอง จะต่างกับ Visual Studio ที่เป็น IDE เพื่อมารองรับการเขียน .NET Core

## **.NET Core vs .NET Framework**

![.NET\_Core-03.png](../../.gitbook/assets/net\_core-03.png)

.NET Core เกิดจากการที่ Microsoft ประกาศ Open Source เทคโนโลยีของ .NET Framework ให้ [.NET Foundation](https://dotnetfoundation.org/) องค์กรกลางเป็นผู้ดูแล แล้วพัฒนาต่อมาเป็น .NET Core เพื่อให้สามารถทำงานแแบบ Cross-Platform ได้ โดยมี Feature แค่บางส่วนของ .NET Framwork ในเวอร์ชั่นแรก ซึ่งแนวทางพัฒนาจะไปทาง .NET Core มากขึ้น เพื่อป้องกันปัญหาจากการย้าย .NET Framework ไปรันบน .NET Core ทาง Microsoft จึงกำหนดมาตรฐานกลาง [.NET Standard](https://dotnet.microsoft.com/platform/dotnet-standard) ขึ้นมา ซึ่งเป็นชุดของ API ที่ทั้ง .NET Core และ .NET Framework จะต้องเรียกใช้

.NET Framework จะเหมาะกับงานด้าน Windows Application ที่ใช้ Windows Forms, WPF และ UWP ส่วน .NET Core จะเหมาะกับงานด้าน Web Application ที่ต้องการ High Performance & Scalable โดยใช้สถาปัตยกรรมแบบ Microservice ซึ่งจะสะดวกกว่า เร็วกว่า รองรับการทำงานแบบ Cross-Platform และ .NET CLI แต่แลกมาด้วย Learning Curve ที่สูงขึ้น แต่เชื่อเถอะว่าง่ายกว่าตอนเขียน Web Application ที่เขียนบน .NET Framework แบบเดิมเยอะ แต่โดยส่วนใหญ่จะใช้ .NET Core ทำเป็น Web API แต่ไม่ว่าจะเป็น .NET Core หรือ .NET Framework

**อ่านเพิ่มเติม** : [https://bit.ly/2xSS0I8](https://bit.ly/2xSS0I8)

## **.NET 5**

![.NET\_Core-04.png](../../.gitbook/assets/net\_core-04.png)

หลังจากการเปิดตัว .NET Core 3.0 ทาง Microsoft ก็ประกาศการเปิดตัวครั้งต่อไปจะเป็น [.NET 5](https://devblogs.microsoft.com/dotnet/introducing-net-5/) ในเดือนพฤศจิกายน 2020 ซึ่งเป็นการรวม .NET Core และ .NET Framework เข้าด้วยกัน โดยจะต้องทำการ Update Visual Studio และ Visual Code ให้รองรับในช่วงครึ่งแรกของปี

**อ่านเพิ่มเติม** : [https://bit.ly/2EACeVZ](https://bit.ly/2EACeVZ)
