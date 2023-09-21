1. โจทย์ข้อ Secret Message 100 point ข้อในให้ไฟล์ .pcap มา ขั้นแรกเลย เราก็ลองอ่านๆ packet ด้วยโปรแกรม Wireshark ดู

![img1](12.png?raw=true)

`ข้อนี้ packet น้อยมากกกก` ดูง่ายๆ 

2. มีแค่ HTTP สังเกต ที่ POST Method มีการอัปไฟล์ขึ้นไป flag.zip ขึ้น

![img1](13.png?raw=true) 

3. ง่ายๆก็ Export HTTP Objects มาดู ไปที่ File > Export Objects > HTTP

![img1](14.png?raw=true)

4. เราจะได้ไฟล์ `upload.php` มา 2 ไฟล์ ผมเลยเอาไฟล์ `upload.php` ไฟล์แรกไปเปิดที่ [HexEd](https://hexed.it/)

![img1](15.png?raw=true)

สังเกต ตรง `50 4B 03 04` ขึ้นต้น PK คุ้นๆแฮะ เหมือนจะเป็นไฟล์ .zip รึป่าวนะ อะเราไปเช็คที่ File signature เลยละกันที่เว็บ [garykessler](https://www.garykessler.net/library/file_sigs.html)

5. แก้ Hex เป็นไฟล์ใหม่เลย ง่ายๆ เราก็ลบข้างหน้า Hex ก่อนถึง `50 4B 03 04` ออกให้หมด ให้มันขึ้นต้นด้วย  `50 4B 03 04` ตามภาพ แล้ว save เป็นไฟล์ `.zip` แทน
 
![img1](16.png?raw=true)

6. ผมก็ทำการ save file ที่แก้ Header แล้ว จาก HexEd มาเป็นชื่อ flagctt.zip แล้วก็ทำการ แตกไฟล์ไปจนได้เป็นไฟล์ flag.txt มาตามภาพ

![img1](17.png?raw=true)

![img1](18.png?raw=true)

7. แต่มันยังไม่ใช้ flag ที่แท้จริงต้องเอาไปถอดรหัสอีก แต่ format มันคล้ายๆคุ้นเหมือนจะเป็น base64 นะ แต่กลับหัวกลับหางอยู่ เอาไปถอดรหัสเว็บสามัญประจำบ้านเลย [cyberchef](https://gchq.github.io/CyberChef/)

   >step Revese >> From Base64 >> ได้ Flag เรียบร้อย
 
![img1](19.png?raw=true)


