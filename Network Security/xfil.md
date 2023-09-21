1. โจทย์ข้อ xfil ของรายการ Cyber Top Talent 2023 (Point 200) 
2. ผู้ออกโจทย์ได้ให้ไฟล์ชื่อ xfil.pcapng มา ให้เราทำการเปิดด้วยโปรแกรม Wireshark

![img1](1.png?raw=true)
3. สังเกต value ค่า Queries ใน packet ที่1 จะพบว่าขึ้นต้นด้วย `ffd8...`

![img1](2.png?raw=true)

ซึ่งเมื่อเห็นในรูปแบบนี้ ทำให้เราคิดถึงในเรื่องของ `file signature` จึงลองเลื่อนลงไปดู packet สุดท้าย พบว่า ลงท้ายด้วย `ffd9` 

![img1](3.png?raw=true)

4. ลองเอาค่า `ffd8` ไป search ใน [garykessler](https://www.garykessler.net/library/file_sigs.html)

![img1](4.png?raw=true)
