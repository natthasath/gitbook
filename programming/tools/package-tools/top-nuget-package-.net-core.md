# 🧶 Top NuGet Package .NET Core

{% hint style="info" %}
สำหรับคนที่ทำงานเกี่ยวกับ Developer โดยใช้ภาษา .NET Core ผมก็จะมาแนะนำ NuGet Package ที่จำเป็นต่อการทำงานด้าน Developer ซึ่งคนที่ทำงานด้านนี้จำเป็นจะต้องรู้จักและศึกษาการใช้งาน ซึ่งผมก็ใช้อยู่ในปัจจุบัน
{% endhint %}

## **Basic Package**

* [Microsoft.AspNetCore.Authentication.JwtBearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer/) : ใช้สำหรับ Authentication ด้วย JWT ผ่านทาง Bearer
* [Swashbuckle.AspNetCore](https://www.nuget.org/packages/Swashbuckle.AspNetCore/) : ใช้สำหรับสร้าง API Document ด้วย Swagger และใช้ในการทดสอบ API Testing
* [Swashbuckle.AspNetCore.Annotations](https://www.nuget.org/packages/Swashbuckle.AspNetCore.Annotations/) : ใช้สำหรับจัดการ Custom Attribute ของ Swagger ด้วย Data Annotation
* [Novell.Directory.Ldap.NETStandard](https://www.nuget.org/packages/Novell.Directory.Ldap.NETStandard/) : ใช้สำหรับเชื่อมต่อ Active Directory ( AD ) ผ่านทาง LDAP ซึ่งรองรับตั้งแต่ .NET Standard 1.3 ขึ้นไป
* [Serilog.Extensions.Logging.File](https://www.nuget.org/packages/Serilog.Extensions.Logging.File/2.0.0-dev-00039) : ใช้สำหรับบันทึก Log บน .NET Core ด้วยคำสั่งที่สั้นกว่า NLog อีกทั้งยังดีกว่าในแง่ของ Performance ไม่ว่าจะเป็น Throughput, Latency
* [AutoMapper Dependency Injection](https://www.nuget.org/packages/AutoMapper.Extensions.Microsoft.DependencyInjection/) : ใช้สำหรับเรียกใช้ AutoMapper ผ่านทาง Dependency Injection เข้ามาใน Constructor ซึ่งเป็นการ Map กันระหว่าง Object กับ Object

## **Database Package**

* [Microsoft.EntityFrameworkCore.Design](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design/) : ใช้สำหรับจัดการ Entity Framework Core ผ่านทาง .NET Core CLI
* [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools/) : ใช้สำหรับจัดการ Entity Framework Core ผ่านทาง Package Manager Console
* [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/) : ใช้สำหรับสร้าง Entity Framework Core เชื่อมต่อฐานข้อมูล Microsoft SQL Server
* [Oracle.EntityFrameworkCore](https://www.nuget.org/packages/Oracle.EntityFrameworkCore/) : ใช้สำหรับสร้าง Entity Framework Core ของฐานข้อมูล Oracle Database ด้วย Oracle Data Provider ( ODP.NET )
* [Oracle.ManagedDataAccess.Core](https://www.nuget.org/packages/Oracle.ManagedDataAccess.Core/) : ใช้สำหรับเชื่อมต่อ Oracle Database แบบ Fast Data Access ด้วย ADO.NET Driver ที่ประกอบด้วย Dynamic-Link Library
* [dotnet-sonarscanner](https://www.nuget.org/packages/dotnet-sonarscanner/) : ให้สำหรับตรวจสอบ Automatic Code Review เพื่อหาข้อผิดพลาดในการเขียนโปรแกรม รวมถึงช่องโหว่ต่าง ๆ

**อ่านเพิ่มเติม** : [https://bit.ly/2RYvvNn](https://bit.ly/2RYvvNn)
