1. โจทย์ข้อ MitM 200 point ข้อนี้ก็มีไฟล์ .pcap มาให้เรา download กัน เราก็เปิดไฟล์ด้วย wireshark เพื่อดูข้อมูลเบื้องต้นก่อน

  เราก็เริ่มจากการดู protocol hierachy เพื่อง่ายต่อการวิเคราะห์ก่อน >>> ผมก็ลองไล่ stream ดู packet / ลองเลื่อนดูผ่านๆตา ก็ไปเจอสิ่งที่มันน่าสนใจคือ มันมีการ พยายาม Log in เข้า Mail ดูตามภาพเลยครับ

![img1](24.png?raw=true)

จะเห็นว่า ใน Value AUTH LOGIN มีค่าคือ QWRtaW5TTVRQ ซึ่งเราลองเอาค่าตรงนี้ไป decode ด้วย base64 จะได้คำว่า `AdminSMTP` เราสันนิษฐานว่านี่น่าจะเป็น Username / Value UGFzc3dvcmQ6 เอาไป decode ด้วย base64 เหมือนเดิมจะเท่ากับ Password: 

เราก็จะรู้แล้วว่า ค่าด้านล่าง ซึ่งคือ UEBzc3cwcmQy น่าจะเป็น Password เราก็ลอง decode ด้วย base64 เหมือนเดิม มีค่าเท่ากับ P@ssw0rd2 แต่เราลองดูที่บรรทัดล่างก็จะเห็นว่า Authentication unsuccessful มันก็คือการพยายาม Brute force รหัสผ่านนั่นเอง

2. จากนั้น ผมก็ลองไล่ stream ดูเรื่อยๆต่อจากเดิม ทำให้เราได้เห็นว่า มันมีค่า Password เปลี่ยน แล้วก็ยัง Fail Authen เหมือนเดิม  

![img1](25.png?raw=true)

3. ผมเลยเลื่อนไปดู packet ล่างๆเลย เพราะคิดว่ามันน่าจะ Brute force สำเร็จ แล้วมันก็ใช่จริงๆ! stream ที่ 502 packet no.8119 เราจะเห็นเลยว่า มัน Login สำเร็จ ด้วย (Username : `AdminSMTP` / Password : V293IVlvdUZvdW5kUGFzc3dvcmQ= decode ด้วย base64 คือ `Wow!YouFoundPassword`)

แถมยังเห็นว่า มีการส่งไฟล์ที่ชื่อว่า secret.docx อีกด้วย (ชื่อไฟล์เป็นหนทางสว่างมาก55555)     

![img1](26.png?raw=true)

4. ด้วยความที่ไม่รู้ว่าจะเปิดอ่านไฟล์ `secret.docx` ยังไง ผมเลยใช้ตัวช่วยคืออออออ!! [NetworkMiner](https://www.netresec.com/?page=NetworkMiner) โคตรจะมีประโยชน์ โปรแกรมนี้มันจะช่วยเราในการ วิเคราะห์ข้อมูลต่างๆในไฟล์ .pcap เราไม่ต้องมานั่งไล่ดู มันสรุปมาให้เลยย

  ผมก็เอาไฟล์ .pcap ข้อนี้ไปเปิดเลย

![img1](27.png?raw=true)

ไปที่ Tab File จะเห็นว่ามันมีไฟล์อยู่ 2 ไฟล์ เราก็เปิดไฟล์ขึ้นมา คลิกขวา Open file

![img1](28.png?raw=true)

อ่าวววว มันยังไม่จบ มันติด Password ถึงจะเข้าไปอ่านไฟล์นี้ได้ 

![img1](29.png?raw=true)

5. ผมก็เอา Password ที่ได้ บน stream 502 (Wow!YouFoundPassword) ไปใส่เลย แล้วก็ตู้ม ระเบิดเป็นโกโก้ครั้นนนนนนน!!!

![img1](30.png?raw=true)




