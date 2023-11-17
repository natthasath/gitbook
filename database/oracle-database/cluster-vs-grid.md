# 🫑 Cluster vs Grid

{% hint style="info" %}
หากใครเคยทำพวก Distribution Computing ในการประมวลผลข้อมูลแบบกระจาย ที่พัฒนามาจากการประมวลผลข้อมูลแบบรวมศูนย์ Centralize Computing คงจะเคยได้ยิน Cluster และ Grid ซึ่งเป็นการทำ Distribution Computing เหมือนกัน แต่การใช้งานไม่เหมือนกัน
{% endhint %}

<figure><img src="../../.gitbook/assets/_59a0f326-8d28-4dc6-9439-688667b318f4.jpg" alt=""><figcaption></figcaption></figure>

## **Cluster Computing**

Cluster หมายถึง กลุ่มของเครื่องคอมพิวเตอร์ตั้งแต่ 2 เครื่องขึ้นไป ยี่ห้อเดียวกัน รุ่นเดียวกัน เครือข่ายเดียวกัน ( Homogeneous Network ) นำมาเชื่อมต่อผ่าน Fast Local Area Network เดียวกัน เพื่อให้สามารถทำงานทดแทนกันได้ อย่างเช่น VMware, Docker หรือแม้แต่บน Apache Hadoop ซึ่งสามารถตั้งค่าได้ 2 แบบ Active-Active, Active-Passive หรือ Active-Standby แต่ละเครื่องจะมีการ Share Resource และ Manage Resource ผ่านศูนย์กลาง ( Resource Manager ) หากเครื่องตัวใดตัวหนึ่งทำงานหนักไป สามารถย้าย Service ไปทำงานอยู่บนอีกเครื่องหนึ่ง ( Load Balance ) หรือหากเครื่องเกิด Fail Over ก็จะสามารถย้ายไปรันอยู่บนอีกเครื่องหนึ่งตาม Policy ที่เราได้กำหนดไว้ทั้ง 2 แบบ ( Fault Tolerance ) ปัจจุบัน Grid Computing ถูกนำมาใช้ใน Oracle Database ในลักษณะของ Real Application Cluster ( RAC )

## **Grid Computing**

Grid หมายถึง กลุ่มของเครื่องคอมพิวเตอร์ตั้งแต่ 2 เครื่องขึ้นไป ไม่จำเป็นต้องมี ยี่ห้อเดียวกัน รุ่นเดียวกัน เครือข่ายต่างกัน ( Heterogeneous Network ) นำมาเชื่อมต่อผ่าน Internet เพื่อช่วยกันประมวลผล ให้มีความสามารถเทียบได้กับ Supercomputer แต่ละเครื่องจะมีการ Share Resource และ Manage Resource ผ่านตัวมันเอง ปัจจุบัน Grid Computing ถูกนำมาใช้ใน Oracle Database ตั้งแต่เวอร์ชั่น 10g และ 11g

**อ่านเพิ่มเติม** : [https://bit.ly/2m0Ww56](https://bit.ly/2m0Ww56)
