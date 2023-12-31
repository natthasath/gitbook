# 🎩 Best Practice Ransomware Protection

{% hint style="info" %}
หลายคนคงเคยได้ยินข่าวการโจมตีด้วย Ransomware ซึ่งถือเป็นภัยคุกคามทางไซเบอร์ที่ส่งผลกระทบต่อการดำเนินงานขององค์กร เราจึงจะมาทำความรู้จัก Ransomware รวมถึงแนวปฏิบัติในการรับมือภัยคุกคามทางไซเบอร์จาก Ransomware
{% endhint %}

## **🧔🏻 Ransomware**

Ransomware เป็น Malware ประเภทหนึ่ง ที่มีลักษณะต่างจาก Malware ประเภทอื่น คือมันไม่ได้ทำการขโมยข้อมูล แต่จะทำการเข้ารหัสข้อมูลแทน ทำให้ไม่สามารถเรียกดูข้อมูล หรือ กระทำการใด ๆ กับข้อมูลได้ ซึ่งการถอดรหัสได้นั้นจะต้องใช้ Decryption Key แต่จะต้องแลกกับการจ่ายเงินที่ใช้เรียกค่าไถ่ไปยังบัญชีของผู้ไม่ประสงค์ดี

จำนวนเงินที่ถูกเรียกค่าไถ่ก็จะแตกต่างกันไป โดยการจ่ายเงินจะต้องทำผ่านระบบที่ไม่สามารถตรวจสอบหรือติดตามได้ ซึ่งจะนิยมชำระผ่านทาง Cryptocurrency อย่าง BitCoin ที่อาศัยเทคโนโลยีของ Blockchain เพื่อใช้ในการสร้างสกุลเงินดิจิทัล และใช้ทำธุรกรรมบน Internet

## **👮🏻 การแพร่กระจาย**

การแพร่กระจายของ Ransomware ส่วนใหญ่มักจะมาในรูปแบบไฟล์แนบทางอีเมล โดยระบุแหล่งที่มาให้มีความน่าเชื่อถือ อย่างเช่น ธนาคาร หรือ จดชื่อโดเมนให้มีตวามคล้ายคลึงกับเว็บไซต์ที่น่าเชื่อถือให้มากที่สุด ทำให้ถ้าเราไม่สังเกตหรือทำการตรวจสอบก่อน อาจจะเผลอไปคลิกได้ ซึ่งถ้าหากเครื่องคอมพิวเตอร์เครื่องใดเครื่องหนึ่งติด Ransomware เครื่องคอมพิวเตอร์เครื่องอื่น ๆ ที่อยู่ในเครือข่ายเดียวกันก็จะติดไปด้วย

{% hint style="danger" %}
ดังนั้น ถ้าหากเครื่องคอมพิวเตอร์ติด Ransomware ให้ทำการตัดการเชื่อมต่อ ออกจากเครือข่าย โดยการถอดสาย LAN ออก จากนั้นให้ทำการ Format เครื่องคอมพิวเตอร์เครื่องนั้น แล้วค่อยทำการ Restore ข้อมูล
{% endhint %}

## **💂🏻‍♂️ การป้องกัน**

* ไม่ทำการคลิกลิงก์ ดาวนโหลด เปิดไฟล์ จากแหล่งข้อมูลที่ไม่น่าเชื่อถือ หรือ ไม่ทราบแหล่งที่มา และควรคลิกลิงก์ ดาวน์โหลด เปิดไฟล์ จากแหล่งข้อมูลที่น่าเชื่อถือเท่านั้น
* ทำการติดตั้งโปรแกรม Anti Virus พร้อมทำการ Update โปรแกรมให้เป็นเวอร์ชั่นล่าสุดเสมอ เพื่ออัพเดท Virus Signature ใหม่ ๆ
* ทำการสำรองข้อมูล Backup ไปไว้บน Cloud พวก OneDrive, Google Drive หากข้อมูลติด Ransomware ก็จะสามารถดึงข้อมูลที่สำรองไว้มาใช้ได้
* ทำการอัพเดท Patch OS สม่ำเสมอ เพื่อแก้ไขช่องโหว่ของระบบปฏิบัติการ เช่น Windows, Linux, MacOS
* ทำการกำหนดระดับสิทธิการใช้งาน และการเข้าถึงข้อมูลต่าง ๆ รวมถึงการจัดเก็บประวัติการเข้าถึงและแก้ไขข้อมูล
* ทำการตั้งค่า DNS ที่สามารถ Block Malware ได้ เช่น Cloudflare ( 1.1.1.2 และ 1.0.0.2 ), Google ( 8.8.8.8 และ 8.8.4.4 )

## **🕵🏻 เอกสารที่เกี่ยวข้อง**

* [แนวปฏิบัติในการรับมือเหตุการณ์ภัยคุกคามทางไซเบอร์เกี่ยวกับมัลแวร์เรียกค่าไถ่ ( Ransomware ) สำหรับหน่วยงานภาครัฐ](https://www.etda.or.th/getattachment/newsevents/pr-news/ThaiCERT/etda-recommendation-ransomware-guideline/ETDAannounce-29Sep62-guildeline-ransomware.pdf.aspx?lang=th-TH)
* [แบบประเมินตนเอง](https://www.etda.or.th/getattachment/newsevents/pr-news/ThaiCERT/etda-recommendation-ransomware-guideline/20200928\_Ransomware\_Checklist\_Rev1-1.pdf.aspx?lang=th-TH)

**อ่านเพิ่มเติม** : [https://bit.ly/3m1lbAa](https://bit.ly/3m1lbAa)
