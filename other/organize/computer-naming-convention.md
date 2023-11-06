# 💻 Computer Naming Convention

{% hint style="info" %}
ในการตั้งชื่อ Computer Name ขององค์กร ควรจะมีกฏในการตั้งชื่อ เพื่อให้สามารถระบุตำแหน่งที่ตั้ง สำหรับการจัดการทรัพย์สิน หรือ เพื่อให้สามารถระบุตัวผู้ใช้งาน ซึ่งจะมีประโยชน์ในการระบุตัวผู้กระทำความผิดตาม พ.ร.บ.คอมพิวเตอร์ รวมถึงมีประโยชน์ในการแก้ไขปัญหาการให้บริการต่าง ๆ
{% endhint %}

## **😚 ตั้งชื่อแบบ** **Identify User**

> Department-Username-Device

```
IT-NATTHASATH-PC   // Desktop
IT-NATTHASATH-NB   // Notebook
```

## **🤔 ตั้งชื่อแบบ Scalable**

> Building-Department-Device-AssetNo

```
B1-IT-PC-0001   // Desktop
B1-IT-NB-0002   // Notebook
```

การเชื่อมคำต่าง ๆ จะใช้ ( – ) หรือ ( \_ ) ในการเชื่อมคำ การตั้งชื่อจะใช้ตัวเล็กหรือตัวใหญ่ก็ได้ ( Case-insensitive ) แต่ผมแนะนำให้ใช้ตัวใหญ่จะดูง่ายกว่า นอกจากนี้ ในกรณีที่มีสาขา อาจจะเอา Branch ขึ้นก่อน Building ก็ได้ แต่ถ้าสาขาทำ Domain แยก Forest กันก็ไม่จำเป็นต้องระบุสาขาก็ได้
