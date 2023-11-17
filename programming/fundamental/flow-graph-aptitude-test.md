# 🟡 Flow Graph Aptitude Test

{% hint style="info" %}
Aptitude Test เป็นข้อสอบที่ใช้วัดการแก้ปัญหา ซึ่งใช้ในการทดสอบรับสมัครพนักงานตามบริษัทต่าง ๆ บริษัทด้านไอทีก็เช่นเดียวกัน แต่จะใช้แบบทดสอบที่ต่างออกไปในลักษณะของ Flow Graph Aptitude Test โดยจะต้องนำข้อมูลและเงื่อนไขที่โจทย์กำหนด มาใช้ในการหาคำตอบ
{% endhint %}

## **🐲 Flow Graph Aptitude Test**

โจทย์ลักษณะนี้จะไม่เหมือนกับ Data Flow Diagram แต่จะคล้าย ๆ กัน ซึ่งมันสามารถอยู่ในลักษณะของเลขอนุกรม ( Numerical ), แผนภาพ ( Diagrammatic ) ที่มีการวน Loop โดยโจทย์ที่ใช้ในการรับสมัครพนักงานจะเป็นภาษาอังกฤษ

### **🫎 Example**

ตัวอย่างโจทย์ที่พอหาได้ [Flow Graph Aptitude Test](https://bit.ly/345rJ7Q) เนื่องจากจำโจทย์ที่เคยทำตอนหางานครั้งแรก ๆ ไม่ได้แล้ว แต่หากใครอยากลองทำโจทย์แนวนี้ของจริง ให้ไปสมัครงานตำแหน่งพวก Developer, Programmer อย่าง CDG ไม่รู้ยังใช้แบบทดสอบนี้อยู่มั้ย

{% code overflow="wrap" %}
```
Consider 8 boxes with following values
Box 1 = 2
Box 2 = 7
Box 3 = 2
Box 4 = 1
Box 5 = 5
Box 6 = 7
Box 7 = 1
Box 8 = 4

Now follow the instructions:

1. Put the number from Box 7 into Box 1
2. Add the numbers from Box 1 and Box 2, and put the result in Box 1
3. Change Instruction 2, Increase the number in Box 2 by 1
4. If the second box number mentioned in instruction 2 is greater than the number in box 8, stop. If not, go to step 2.

What number is in Box 1 now?

Note: When you are told to put a number into a box, it is understood that whatever number was previously in that box has just been erased.
```
{% endcode %}

### **🦄 Problem solving**

สิ่งแรกที่ต้องทำคือแปลโจทย์จากอังกฤษเป็นไทย อ่านโจทย์แบบคร่าว ๆ ทั้งหมดก่อน ว่าโจทย์ให้ทำอะไร แล้วทำการวาดภาพในหัว

* _No. 1 Instruction 1_ นำค่าใน Box 7 ไปใส่ใน Box 1 จะได้ _**Box 1 = 1**_

```
b[1] = b[7]
b[1] = 1
```

* _No. 1 Instruction 2_ นำค่าใน Box 1 และ Box 2 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1 จะได้ _**Box 1 = 8**_

```
b[1] = b[1] + b[2]
b[1] = 1 + 7 = 8
```

* _No. 1 Instruction 3_ เปลี่ยนเงื่อนไขที่ 2 เพิ่มค่าใน Box 2 ขึ้นมา 1 จะได้ _**Box 2 = 8**_

```
b[2] = b[2] + 1
b[2] = 7 + 1 = 8
```

* _No. 1 Instruction 4_ ถ้าค่าใน Box 2 ในเงื่อนไขที 2 มีค่ามากกว่า ค่าใน Box 8 ให้หยุด ถ้าไม่ใช่ให้กลับไปทำเงื่อนไขที่ 2 จะได้ _**True**_ ทำให้ต้องหยุดการทำงาน

```
b[2] > b[8]
8 > 4
```

* _Incorrect Answer_ คำตอบไม่ถูกต้อง นั่นเป็นเพราะเราแปลโจทย์ข้อ 3 ผิด ซึ่งเราจะสับสนระหว่าง _**number from Box**_ กับ _**number in Box**_

```
b[1] = Answer
b[1] = 8
```

* _Fix No. 1 Instruction 3_ เปลี่ยนเงื่อนไขที่ 2 เพิ่ม Box 2 ขึ้นมา 1 จะได้ Instruction ใหม่เป็นการนำค่าใน Box 1 และ Box 3 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1

```
b[1] = b[1] + b[2 + 1]
b[1] = b[1] + b[3]
```

* _Fix No. 1 Instruction 4_ ถ้าค่าใน Box 3 ในเงื่อนไขที 2 มีค่ามากกว่า ค่าใน Box 8 ให้หยุด ถ้าไม่ใช่ให้กลับไปทำเงื่อนไขที่ 2 จะได้ _**False**_ ทำให้ต้องกลับไปทำเงื่อนไขที่ 2

```
b[3] < b[8]
3 < 4
```

* _No. 2 Instruction 2_ นำค่าใน Box 1 และ Box 3 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1 จะได้ **Box 1 = 10**\


```
b[1] = b[1] + b[3]
b[1] = 8 + 2 = 10
```

* _No. 2 Instruction 3_ เปลี่ยนเงื่อนไขที่ 2 เพิ่ม Box 3 ขึ้นมา 1 จะได้ Instruction ใหม่เป็นการนำค่าใน Box 1 และ Box 4 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1

```
b[1] = b[1] + b[3 + 1]
b[1] = b[1] + b[4]
```

* _No. 2 Instruction 4_ ถ้าค่าใน Box 4 ในเงื่อนไขที 2 มีค่ามากกว่า ค่าใน Box 8 ให้หยุด ถ้าไม่ใช่ให้กลับไปทำเงื่อนไขที่ 2 จะได้ _**False**_ ทำให้ต้องกลับไปทำเงื่อนไขที่ 2

```
b[4] < b[8]
1 < 4
```

* _No.3 Instruction 2_ นำค่าใน Box 1 และ Box 4 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1 จะได้ **Box 1 = 11**

```
b[1] = b[1] + b[4]
b[1] = 10 + 1 = 11
```

* _No. 3 Instruction 3_ เปลี่ยนเงื่อนไขที่ 2 เพิ่ม Box 4 ขึ้นมา 1 จะได้ Instruction ใหม่เป็นการนำค่าใน Box 1 และ Box 5 บวกกัน แล้วนำผลลัพธ์ไปใส่ใน Box 1

```
b[1] = b[1] + b[4 + 1]
b[1] = b[1] + b[5]
```

* _No. 3 Instruction 4_ ถ้าค่าใน Box 5 ในเงื่อนไขที 2 มีค่ามากกว่า ค่าใน Box 8 ให้หยุด ถ้าไม่ใช่ให้กลับไปทำเงื่อนไขที่ 2 จะได้ **True** ทำให้หยุดการวน Loop

```
b[5] < b[8]
5 < 4
```

* _Correct Answer_ คำตอบที่ถูกต้องคือ **Box 1 = 11**

```
b[1] = Answer
b[1] = 11
```
