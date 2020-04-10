## **CN210**

ที่นี่เป็นแหล่งรวม Link YouTube ที่สรุปเนื้อหาการเรียนในรายวิชา CN210 : Fundamental of computer architecture ที่ สิริกร แสงโชคานนท์ 6110613053 จัดทำขึ้น โดยแบ่งเป็นแต่ละหัวข้อตามด้านล่างนี้


### CLIP

* [CLIP 1](https://youtu.be/4FirKjjTNqQ) **R-Format**

R- format เป็นคำสั่งประเภทหนึ่งของ MIPS ซึ่งมี 32-bit มี 6 ส่วน

|op | rs | rt | rd | shamt | func |
|---|---|---|---|---|---|
|6-bit|5-bit|5-bit|5-bit|5-bit|6-bit|

   
*func $rd, $rs, $rt*
   
ทำหน้าที่คำนวณข้อมูลที่เก็บไว้ที่ register rs และ register rt แล้วนำผลลัพธ์ที่ได้จากการคำนวณไปเก็บไว้ที่ register rd โดย func เป็นตัวกำหนดการคำนวณ ( +, - ,...) ในส่วนของ op ในคำสั่งประเภท R-Format จะมีค่าเป็น 0 ทั้ง 6-bit


* [CLIP 2](https://youtu.be/baCNeNydnZY) **CPU**

ยกตัวอย่างการทำงานของ MIPS CPU ตั้งแต่การเปิดเครื่องคอมพิวเตอร์ขึ้นมา โดยเริ่มจากการดูว่าตำแหน่งเริ่มต้นของ CPU ชี้ไปที่ Address ใด ซึ่งตำแหน่งเริ่มต้นอาจไม่ใช่ตำแหน่ง 0 เสมอไป จากนั้นให้ทำงานตามคำสั่งที่เก็บไว้ใน Address นั้นๆ 1 คำสั่งมี 4-bit ดังนั้นเมื่อทำงานจบ 1 คำสั่งแล้วก็จะไปทำคำสั่งที่ 4-bit ถัดไป ใน CLIP จะประกอบไปด้วยคำสั่งทั้ง 3 ประเภท ของ MIPS ได้แก่ R-Format, I-Format และJ-Format มีรายละเอียดดังต่อไปนี้ 

   1. R-Format มี 6 ส่วน *(อธิบายไปแล้วในหัวข้อ CLIP 1 ด้านบน)*
      
   2. I-Format มี 4 ส่วน ใช้ในการเคลื่อนย้ายข้อมูลที่เก็บไว้ใน register
   
|op | rs | rt | value or offset |
|---|---|---|---|
|6-bit|5-bit|5-bit|16-bit|

*lw $rt, offset($rs)* , *sw $rt, offset($rs)*

   3. J-Format มี 2 ส่วน ใช้ในการ jump จากตำแหน่ง Address ปัจจุบันไปยังอีกตำแหน่งหนึ่ง
   
|op | absolute address |
|---|---|
|6-bit|26-bit|

*j address*

* [CLIP 3](https://youtu.be/vtOKFp1MgOQ) **Single cycle VS Multi-cycle**

Single cycle : วงจร digital ที่อ่านและทำงานตามคำสั่งจบได้ใน 1 cycle (cycle = clock ของคอมพิวเตอร์) หรือสรุปสั้นๆได้ว่า 1 คำสั่งจบได้ใน 1 cycle และไม่ว่าจะทำคำสั่งใดจะใช้เวลาเท่ากันทั้งหมดคือ 8ns มี ALU มากกว่า 1 memory แบ่งเป็น 2 ส่วน คือ instruction memory และ data memory
![image](https://i.stack.imgur.com/vCvw1.png)

Multi-cycle  : วงจร digital ที่อ่านและทำงานตามคำสั่งจบในหลาย cycle เวลาในการทำแต่ละคำสั่งจะไม่เท่ากัน มี ALU 1 ตัว  instruction memory และ data memory รวมเป็นอันเดียวกัน มี Instruction register และ A, B พักข้อมูลจาก register ก่อนเข้าไปคำนวณใน ALU
![image](https://i.imgur.com/mWXHWpT.png)

* [CLIP 4](https://youtu.be/4qoSZZjcNaI) **lw in Multi-cycle**

lw เป็นคำสั่งประเภท I- format *(อธิบายไปแล้วในหัวข้อ CLIP 2 ด้านบน)*

ซึ่งใน muti-cycle คำสั่ง lw มีทั้งหมด 5 cycle ดังต่อไปนี้
```
   T1 IR = Memory[PC]              #อ่านว่าปัจจุบัน PC ชี้ไปที่ Address ใดใน Memory แล้วนำไปเก็บไว้ที่ Instruction Register
      PC = PC + 4                  #นำ PC ปัจจุบันบวก 4 เพื่อเตรียมตัวทำคำสั่งถัดไป เพราะ 1 คำสั่งใช้ 4 bytes
   T2   = Reg[IR[25-21]]
   
```
### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/SirikornBeauty/CN210-CLIP/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
