## CN210

ที่นี่เป็นแหล่งรวม Link YouTube ที่สรุปเนื้อหาการเรียนในรายวิชา CN210 : Fundamental of computer architecture ที่ สิริกร แสงโชคานนท์ 6110613053 จัดทำขึ้น โดยแบ่งเป็นแต่ละหัวข้อตามด้านล่างนี้


### CLIP

* [CLIP 1](https://youtu.be/4FirKjjTNqQ) **R-Format**

R- format เป็นคำสั่งประเภทหนึ่งของ MIPS ซึ่งมี 32-bit มี 6 ส่วน

|op | rs | rt | rd | shamt | func |
---|---|---|---|---|---|
6-bit|5-bit|5-bit|5-bit|5-bit|6-bit|

   
*func $rd, $rs, $rt*
   
ทำหน้าที่คำนวณข้อมูลที่เก็บไว้ที่ register rs และ register rt แล้วนำผลลัพธ์ที่ได้จากการคำนวณไปเก็บไว้ที่ register rd โดย func เป็นตัวกำหนดการคำนวณ ( +, - ,...) ในส่วนของ op ในคำสั่งประเภท R-Format จะมีค่าเป็น 0 ทั้ง 6-bit

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/SirikornBeauty/CN210-CLIP/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
