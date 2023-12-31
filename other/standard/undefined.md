# 🎁 มาตรฐานข้อมูลกลาง

## การจัดทำมาตรฐานข้อมูลกลาง

{% hint style="success" %}
ในการจัดทำมาตรฐานข้อมูลของหน่วยงานภาครัฐ ควรดำเนินการตามกรอบแนวทางการเชื่อมโยงรัฐบาลอิเล็กทรอนิกส์แห่งชาติ TH e-GIF โดยมีวัตถุประสงค์ให้หน่วยงานสามารถแลกเปลี่ยนข้อมูลระหว่างหน่วยงานได้อย่างมีประสิทธิภาพ เป็นมาตรฐานเดียวกัน มีความปลอดภัย รวมถึงรองรับการ Migrate Data ในอนาคต โดยมีเป้าหมายที่ประชาชนหรือผู้รับบริการเป็นศูนย์กลางการให้บริการ
{% endhint %}

{% embed url="https://datastandard.dcy.go.th/" %}

## กรอบแนวทางการเชื่อมโยงรัฐบาลอิเล็กทรอนิกส์แห่งชาติ

> (Thailand e-Government Interoperability Framework : TH e-GIF)

{% hint style="success" %}
การเชื่อมโยงกระบวนการทำงานและข้อมูลของระบบงานคอมพิวเตอร์หรือระบบงานอิเล็กทรอนิกส์ของหน่วยงานต่างๆ ทั้งในระดับกอง สำนัก ฝ่าย ศูนย์ กรม กระทรวง และอื่นๆ โดยอาจเป็นการเชื่อมโยงกันภายในหน่วยงาน หรือข้ามหน่วยงาน เพื่อให้สามารถดำเนินธุรกรรมที่มีกระบวนการทำงานและข้อมูลต่างๆ ร่วมกัน ในรูปแบบอิเล็กทรอนิกส์ โดยมีเป้าหมายที่ประชาชนหรือผู้ใช้บริการเป็นศูนย์กลางการให้บริการ ทั้งนี้กระบวนการทำงานและข้อมูลต่างๆ อาจมีความสัมพันธ์ในเชิงธุรกรรมเดียวกันผ่านระบบธุรกรรมอิเล็กทรอนิกส์แบบให้บริการแบบเบ็ดเสร็จ หรือมีหลายบริการร่วมกับในระบบหน้าต่างบริการเดียวกัน
{% endhint %}

## รูปแบบมาตรฐานในการเชื่อมต่อ

{% hint style="success" %}
รูปแบบมาตรฐานในการเชื่อมต่อ ทางหน่วยงานได้จัดทำ Web API ไว้ให้เชื่อมต่อ ข้อมูลจะอยู่ในรูปแบบ JSON โดยทุกครั้งที่มีการเชื่อมต่อจะต้องทำการ Authentication ผ่าน xxx ด้วย Secret Key
{% endhint %}

## คำอธิบายรายละเอียดของรายการข้อมูล

<table><thead><tr><th width="204">ชื่อฟิลด์</th><th>คำอธิบาย</th></tr></thead><tbody><tr><td>วันที่ออกแบบ</td><td>ใส่วันที่ออกแบบ (DD/MM/YYYY) ปีคริสตศักราช</td></tr><tr><td>วันที่แก้ไขล่าสุด</td><td>ใส่วันที่แก้ไขล่าสุด (DD/MM/YYYY) ปีคริสตศักราช</td></tr><tr><td>ชื่อข้อมูล</td><td>ใส่ชื่อรายการข้อมูล (ภาษาไทย)</td></tr><tr><td>คำอธิบาย</td><td>ใส่คำอธิบายรายการข้อมูล (ภาษาไทย) เขียนให้ละเอียด</td></tr><tr><td>ชื่อ</td><td>ใส่ชื่อป้ายกำกับรายการข้อมูล Tag (ภาษาอังกฤษ)</td></tr><tr><td>เป็นส่วนหนึ่งของ</td><td>ใส่ชื่อรายการข้อมูลที่รายการข้อมูลนั้นเป็นองค์ประกอบ</td></tr><tr><td>รูปแบบข้อมูล</td><td>ใส่รูปแบบการจัดเก็บรายการข้อมูล</td></tr><tr><td>ชนิดข้อมูล</td><td>ใส่ชนิดรายการข้อมูล</td></tr><tr><td>ความถี่ที่เกิดขึ้น</td><td>หมายถึง Multiplicity แสดงจำนวนครั้งต่ำสุดถึงสูงสุดของรายการข้อมูลนั้น ตัวเลขทางขวาแสดงตัวเลขต่ำสุดที่รายการข้อมูลนั้นมีได้ และตัวเลขทางซ้ายแสดงตัวเลขสูงสุดที่รายการข้อมูลนั้นมีได้</td></tr><tr><td>อ้างอิงจาก</td><td>ใส่มาตรฐาน หรือพระราชบัญญัติ, กฎหมาย, ระเบียบ ที่เกี่ยวข้องกับรายการข้อมูล</td></tr><tr><td>หน่วยงานเจ้าของข้อมูล</td><td>ใส่ชื่อหน่วยงานที่เป็นเจ้าของรายการข้อมูล</td></tr><tr><td>แหล่งข้อมูลที่เกี่ยวข้อง</td><td>ใส่ชื่อแหล่งข้อมูลที่เกี่ยวข้องที่สามารถศึกษาเพิ่มเติมได้ และตัวอย่างรายละเอียดข้อมูล</td></tr><tr><td>คำแนะนำในการใช้</td><td>ใส่คำแนะนำการใช้รายการข้อมูล</td></tr><tr><td>กฎเพื่อการตรวจสอบ</td><td>ใส่คำแนะนำในการตรวจสอบเพื่อความถูกต้องของรายการข้อมูล</td></tr></tbody></table>

**อ่านเพิ่มเติม** : [https://bit.ly/48DItoQ](https://bit.ly/48DItoQ)
