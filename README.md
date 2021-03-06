# **CN210 : Fundamental of computer architecture**

## **สรุปเนื้อหา**

**Computer** ประกอบด้วย 

   1.Central Processing Unit (CPU) ซึ่งประกอบด้วย 
   
   * Artimetric and logic unit (ALU) 
      
   * Register
      
   * Control Unit
   
   2.Main memory
   
   3.Input/Output
   
   ![image](https://www.computerscience.gcse.guru/wp-content/uploads/2016/04/Von-Neumann-Architecture-Diagram.jpg)
 
 **Von Neumann architecture & Harvard architecture**
 
   * Von Neumann architecture จะรวม instructions memory และ data memory ไว้เป็น memory เดียวกัน
   
   * Harvard architecture จะแยก instructions memory และ data memory เป็นคนละอัน
   
![image](https://media.springernature.com/original/springer-static/image/chp%3A10.1007%2F978-3-030-30367-9_2/MediaObjects/471053_1_En_2_Fig9_HTML.png)

**CISC VS RISC**

   * CISC (Complex Instruction Set Computer) เป็น multi-cycle มีรูปแบบคำสั่งหลากหลาย
   
   * RISC (Reduced Instruction Set Computer) เป็น single cycle มีรูปแบบคำสั่งคงที่ 32-bit
   
*CISC นั้นซับซ้อนและมีแนวโน้มที่จะช้ากว่า RISC แต่ใช้รอบน้อยลงโดยมีคำสั่งน้อยลง*
   
**MIPS** เป็น CPU ที่เลือกมาศึกษาในรายวิชา CN210 ซึ่งแต่ละคำสั่ง 32-bit เท่ากันหมด

   * **ALU Control Bits** ใน MIPS เป็นดังตารางนี้
   
   ![image](https://www.cs.ucr.edu/~windhs/lab4/inc/fig_alu_control_0.png)
   
   
   
   * **Control units** ใน MIPS เป็นดังตารางนี้
   
   ![image](https://raw.githubusercontent.com/SirikornBeauty/CN210-CLIP/master/1.png)
   



### **การบ้าน CLIP**

* [CLIP 1](https://youtu.be/4FirKjjTNqQ) **R-Format**

R- format เป็นคำสั่งประเภทหนึ่งของ MIPS ซึ่งมี 32-bit มี 6 ส่วน ใช้ในการคำนวณทางคณิตศาสตร์

|op | rs | rt | rd | shamt | func |
|---|---|---|---|---|---|
|6-bit|5-bit|5-bit|5-bit|5-bit|6-bit|
   
`func $rd, $rs, $rt`

![image](https://www.cs.ucr.edu/~windhs/lab4/inc/fig_alu_control_lines.png)
   
ทำหน้าที่คำนวณข้อมูลที่เก็บไว้ที่ register rs และ register rt แล้วนำผลลัพธ์ที่ได้จากการคำนวณไปเก็บไว้ที่ register rd โดย func เป็นตัวกำหนดการคำนวณ ( +, - ,...) ในส่วนของ opcode ในคำสั่งประเภท R-Format จะมีค่าเป็น 0 ทั้ง 6-bit



* [CLIP 2](https://youtu.be/baCNeNydnZY) **CPU**

ยกตัวอย่างการทำงานของ MIPS CPU ตั้งแต่การเปิดเครื่องคอมพิวเตอร์ขึ้นมา โดยแปลงภาษาระดับสูงที่มนุษย์สามารถเข้าใจได้ เป็นภาษาเครื่องให้คอมพิวเตอร์ทำงาน 

โดยเริ่มจากการดูว่าตำแหน่งเริ่มต้นของ CPU เมื่อเริ่มเปิดเครื่องคอมพิวเตอร์ชี้ไปที่ Address ใด ซึ่งตำแหน่งเริ่มต้นอาจไม่ใช่ตำแหน่ง 0 เสมอไป จากนั้นให้ทำงานตามคำสั่งที่เก็บไว้ใน Address นั้นๆ 1 คำสั่งมี 4-bit 

ดังนั้นเมื่อทำงานจบ 1 คำสั่งแล้วก็จะไปทำคำสั่งที่ 4-bit ถัดไป 

```

00000000: 8C090004 

จะเห็นว่าที่ Address 00000000 มีคำสั่ง 8C090004 ที่เมื่อแปลงเป็นเลขฐานสองจะได้ 1000 1100 0000 1001 0000 0000 0000 0100

  op      rt      rs       value or offset
100011   00000   01001   0000 0000 0000 0100 

พิจารณาที่ 6-bit แรก จะทราบว่าเป็นคำสั่งประเภท I-Format : lw

rs : 00000 >>> 0
rt : 01001 >>> 9
value or offset : 0000 0000 0000 0100 >>> 4

จะได้ว่า 8C090004  >>>  1000 1100 0000 1001 0000 0000 0000 0100  >>>  lw $9, $0(4) นั่นเอง

```

ใน CLIP จะประกอบไปด้วยคำสั่งทั้ง 3 ประเภท ของ MIPS ได้แก่ R-Format, I-Format และJ-Format มีรายละเอียดดังต่อไปนี้ 

   1. R-Format มี 6 ส่วน *(อธิบายไปแล้วในหัวข้อ CLIP 1 ด้านบน)*
      
   2. I-Format มี 4 ส่วน ใช้ในการเคลื่อนย้ายข้อมูลที่เก็บไว้ใน register
   
|op | rs | rt | value or offset |
|---|---|---|---|
|6-bit|5-bit|5-bit|16-bit|

`lw $rt, offset($rs)`  

`sw $rt, offset($rs)`

   3. J-Format มี 2 ส่วน ใช้ในการ jump จากตำแหน่ง Address ปัจจุบันไปยังอีกตำแหน่งหนึ่ง
   
|op | absolute address |
|---|---|
|6-bit|26-bit|

`j address`

`jal address`





* [CLIP 3](https://youtu.be/vtOKFp1MgOQ) **Single cycle VS Multi-cycle**

**Single cycle** : วงจร digital ที่อ่านและทำงานตามคำสั่งจบได้ใน 1 cycle (cycle = clock ของคอมพิวเตอร์) หรือสรุปสั้นๆได้ว่า 1 คำสั่งจบได้ใน 1 cycle

และไม่ว่าจะทำคำสั่งใดจะใช้เวลาเท่ากันทั้งหมดคือ 8ns 

มี ALU มากกว่า 1 memory แบ่งเป็น 2 ส่วน คือ instruction memory และ data memory
![image](https://i.stack.imgur.com/vCvw1.png)

**Multi-cycle**  : วงจร digital ที่อ่านและทำงานตามคำสั่งจบในหลาย cycle 

เวลาในการทำแต่ละคำสั่งจะไม่เท่ากัน 

มี ALU 1 ตัว  instruction memory และ data memory รวมเป็นอันเดียวกัน 

มี Instruction register และ A, B พักข้อมูลจาก register ก่อนเข้าไปคำนวณใน ALU
![image](https://i.imgur.com/mWXHWpT.png)



* [CLIP 4](https://youtu.be/4qoSZZjcNaI) **lw in Multi-cycle**

lw เป็นคำสั่งประเภท I- format *(อธิบายไปแล้วในหัวข้อ CLIP 2 ด้านบน)*

ซึ่งใน muti-cycle คำสั่ง lw มีทั้งหมด 5 cycle ดังต่อไปนี้
```
   T1 - IR = Memory[PC]                     อ่านว่าปัจจุบัน PC ชี้ไปที่ Address ใดใน Memory แล้วนำไปเก็บไว้ที่ Instruction Register 
        PC = PC + 4                         นำ PC ปัจจุบันบวก 4 เพื่อเตรียมตัวทำคำสั่งถัดไป เพราะ 1 คำสั่งใช้ 4 bytes 
        
   T2 - A  = Reg[IR[25-21]]                 นำข้อมูลที่ register rs ไปเก็บไว้ที่ A
        B  = Reg[IR[20-16]]                 นำข้อมูลที่ register rt ไปเก็บไว้ที่ B
        ALUout = PC + (sign-extend(IR[15-0])<<2)  
        
   T3 - ALUout = A + sign-extend(IR[15-0])  นำค่าที่ A เก็บไว้มาบวกกับ offset แล้วเก็บผลลัพธ์ที่ได้ไว้ใน ALUout
   
   T4 - MDR = Memory[ALUout]                นำผลลัพธ์จาก ALUout มาเก็บไว้ที่ Memory data register
   
   T5 - Reg[IR[20-16]] = MDR                นำค่าที่เก็บไว้ที่ Memory data register มาเก็บใน register rt ซึ่งคือ B
   
```


* [CLIP 5](https://youtu.be/2WN31O6TdE4) **beq in Multi-cycle**

beq เป็นคำสั่งประเภท I- format มี 4 ส่วน *(อธิบายไปแล้วในหัวข้อ CLIP 2 ด้านบน)*  เป็นคำสั่ง jump แบบมีเงื่อนไข โดยจะดูว่าข้อมูลที่ register rs และ register rt เท่ากันหรือไม่ หากเท่ากันจะทำการ jump ไปยังตำแหน่งถัดไป

`beq $rs, $rt, offset`

`bne $rs, $rt, offset`

ซึ่งใน muti-cycle คำสั่ง beq มีทั้งหมด 3 cycle ดังต่อไปนี้
```
   T1 - IR = Memory[PC]                     อ่านว่าปัจจุบัน PC ชี้ไปที่ Address ใดใน Memory แล้วนำไปเก็บไว้ที่ Instruction Register 
        PC = PC + 4                         นำ PC ปัจจุบันบวก 4 เพื่อเตรียมตัวทำคำสั่งถัดไป เพราะ 1 คำสั่งใช้ 4 bytes 
        
   T2 - A  = Reg[IR[25-21]]                 นำข้อมูลที่ register rs ไปเก็บไว้ที่ A
        B  = Reg[IR[20-16]]                 นำข้อมูลที่ register rt ไปเก็บไว้ที่ B
        ALUout = PC + (sign-extend(IR[15-0])<<2)  
        
   T3 - if(A==B) then PC = ALUout           นำค่าที่ A และ B มาเปรียบเทียบกัน หากเท่ากันจะเก็บผลลัพธ์ที่ได้ไว้ใน ALUout ถ้าไม้จะข้ามไปทำคำสั่งถัดไปทันที
   
```



* [CLIP 6](https://youtu.be/kUeTkPxn3ps) **control signal R-format**

![image](https://raw.githubusercontent.com/SirikornBeauty/CN210-CLIP/master/Screenshot%20(206).png)
   
อธิบายการทำงาน control signal ของคำสั่ง R-format ทั้ง 4 cycle ดังนี้ 

```
   T1 - MemRead = 1                   Memory มีการใช้งาน
        IorD = 1                      อ่านว่าปัจจุบัน PC ชี้ไปที่ Address ใดใน Memory
        IRWrite = 1                   นำMemory ที่ถูกชี้ไปเก็บไว้ที่ Instruction Register
        ALUSrcA = 0                   Mux เลือกค่าจาก 0 ซึ่งคือ PC
        ALUSrcB = 1                   Mux เลือกค่าจาก 1 ซึ่งคือ 4
        ALUOP = ADD                   ทำการคำนวณโดยการบวกค่า PC กับ 4
        PCWrite = 1, PCSource = 1     นำผลลัพธ์การคำนวณเขียนทับ PC ปัจจุบัน
        
   T2 - ALUSrcA = 0                   Mux เลือกค่าจาก 0 ซึ่งคือ PC
        ALUSrcB = 3                   Mux เลือกค่าจาก 3 ซึ่งคือ offset
        ALUOP = 0                     ทำการคำนวณโดยการบวกค่า PC กับ offset
        
   T3 - ALUSrcA = 1                   Mux เลือกค่าจาก 1 ซึ่งคือ register rs
        ALUSrcB = 0                   Mux เลือกค่าจาก 0 ซึ่งคือ register rt
        ALUOP = 2                     ทำการคำนวณโดย func เป็นตัวกำหนดว่าจะคำนวณโดยวิธีใด
        
   T4 - RegWrite = 1                  นำ ALUout มาเขียนใน register rd
        MemtoReg = 0                  Mux เลือกค่าจาก 0 ซึ่งคือ ALUout
        RegDst = 1                    Mux เลือกค่าจาก 1 ซึ่งคือ register rd
   
```



* [CLIP 7](https://youtu.be/_eAWHYDgl4w) **Pipelining**

Pipelining คือ หน่วยความจำที่อยู่ระหว่าง CPU และ Memory ทำหน้าที่เก็บคำสั่ง และลำดับคำสั่งโดยการนำคำสั่งที่ต้องทำงานถัดไปมาต่อรอคำสั่งที่กำลังทำงานอยู่ปัจจุบันไม่ให้ CPU ว่าง สามารถทำคำสั่งถัดไปได้เลยโดยที่คำสั่งแรกยังไม่เสร็จ ทำให้ทำงานได้**เร็วขึ้น** 

ยกตัวอย่างการเปรียบเทียบการทำงานของ Pipelining เมื่อ

```
ผ้า 1 ถุง = 1 คำสั่ง 
1 คำสั่ง = 4 ขั้นตอน
1 ขั้นตอน = 30 นาที
```

![image](http://3.bp.blogspot.com/-6RQaYhlYk2k/UKTYQVX9csI/AAAAAAAAAGQ/0xF1OxF_N_Y/s1600/02-What-is-pipelining-01.png)

![image](http://2.bp.blogspot.com/-4YXOlZ30iCQ/UKTYR4Y4FLI/AAAAAAAAAGk/pCdSkaaazVA/s1600/02-What-is-pipelining-02.png)

จากภาพจะเห็นว่า Pipelining ที่ทำงานโดยนำคำสั่งถัดไปมาทำต่อเลย เมื่อจบขั้นตอนที่ 1 ของคำสั่งแรก แล้วทำขั้นตอนที่ 1 ของคำสั่งถัดไปต่อทันทีโดยที่คำสั่งแรกยังไม่เสร็จ ทำให้ประหยัดเวลาขึ้นเมื่อเทียบกับการที่ไม่ใช้ Pipelining

เปรียบเทียบการทำงานแต่ละคำสั่งของ Single cycle, Multi-cycle และ Pipelining ดังภาพนี้

![image](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F22435E39590CA02344037F)
 
