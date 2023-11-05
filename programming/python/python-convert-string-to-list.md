# 🐍 Python Convert String to List

{% hint style="info" %}
ในบางกรณีเราจำเป็นต้องแปลงค่า Parameter ที่ส่งมา อย่างการแปลงค่า String เป็น List ซึ่งในการทำ Web API จะไม่มี Type ของข้อมูลที่เป็น List จะมีแต่ Text, Text ( Multiple Line ), File การจะทำให้ข้อมูลที่รับมาเป็น String เป็น List จะต้องมีการแปลงค่า
{% endhint %}

## **Get Started**

* ฟังก์ชั่น Strip จะลบอักขระทั้งข้างหน้าและข้างหลัง ซึ่งก็คือเครื่องหมายปีกกา \[ ] ส่วนฟังก์ชั่น Split จะแบ่งข้อมูล ซึ่งกำหนดเป็น Comma

{% code title="app.py" %}
```
email_list = "[apple@gmail.com, android@gmail.com]"
emails = email_list.strip('][').split(', ')

print("Email List : ", emails)
print(type(emails))
```
{% endcode %}

**อ่านเพิ่มเติม** : [https://bit.ly/3SDZtTQ](https://bit.ly/3SDZtTQ)
