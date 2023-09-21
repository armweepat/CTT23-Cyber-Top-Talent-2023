1. The Puzzle point 100 ข้อนี้ รายการให้ไฟล์ Pcap มา

![img1](6.png?raw=true) 

2. วิเคราะห์ Protocol ต่างๆใน packet โดยไปที่ Tab Statistics > Protocol Hierarchy จะพบว่าส่วนใหญ่เป็น `HTTP` ผมเลยพุ่งเป้าไปที่ Protocol นั้นเป็นพิเศษ

![img1](7.png?raw=true)

3. ลอง Queries เฉพาะ http พบว่า มีการไปเรียกไฟล์ ไฟล์นึงผ่าน Http GET Method

![img1](8.png?raw=true)

4. ผมเลย Export HTTP Objects มาดู โดยไปที่ File > Export objects > HTTP จะได้ไฟล์ชื่อว่า 16.9b8bb247b8364bfb9a03ed9768c66376.png มา

5. เปิดไฟล์ขึ้นมาเป็นภาพนี้

![img1](16.9b8bb247b8364bfb9a03ed9768c66376.png?raw=true)

6. ก็ง่ายๆเลย เป็นภาพ QR Code ที่เป็น AI แต่มันไม่ครบองค์ประกอบ เราลองไปดู `QR Code` ที่สมบูรณ์กัน

![img1](9.png?raw=true) 

7. มันขาด ไอสี่เหลี่ยมพวกนี่ นี่แหละ เราก็เอาไปใส่ ให้ขนาดมันเท่ากันด้วยนะ

![img1](11.png?raw=true)

8. จากนั้นก็ Scan เลย แค่นี้ก็เจอ Flag แล้ว (แต่พอทำ Write up แล้วมันดันสแกนเอา Flag มาดูไม่ได้แฮะ5555 แต่วิธีหาคำตอบได้แบบนี้แหละ)

