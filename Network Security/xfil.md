1. โจทย์ข้อ xfil ของรายการ Cyber Top Talent 2023 (Point 200) 
2. ผู้ออกโจทย์ได้ให้ไฟล์ชื่อ xfil.pcapng มา ให้เราทำการเปิดด้วยโปรแกรม Wireshark

![img1](1.png?raw=true)
3. สังเกต value ค่า Queries ใน packet ที่1 จะพบว่าขึ้นต้นด้วย `ffd8...`

![img1](2.png?raw=true)

ซึ่งเมื่อเห็นในรูปแบบนี้ ทำให้เราคิดถึงในเรื่องของ `file signature` จึงลองเลื่อนลงไปดู packet สุดท้าย พบว่า ลงท้ายด้วย `ffd9` 

![img1](3.png?raw=true)

4. ลองเอาค่า `ffd8` ไป search ใน [garykessler](https://www.garykessler.net/library/file_sigs.html) จะพบว่าเป็นไฟล์ .JPG

![img1](4.png?raw=true)

5. เขียน python เพื่อดึง value ของ parameter ค่า Queries ไปเปลี่ยนเป็นไฟล์ .jpg ซึ่งคือไฟล์รูปภาพ (ถ้าใครขยัน Copy เอาแล้วก็เอาไปสร้างไฟล์ใหม่ใน [HexEd](https://hexed.it/) ก็ได้ แต่มัน 218 packet นะ5555 เลยให้พี่เป้ย เทพโปรแกรมมิ่ง เขียนโค้ดดึงให้)

```python
from scapy.all import PcapReader, IP ,ICMP
import numpy as np
import codecs
pcapng_file = 'xfil.pcapng'
desired_src_ip = '172.16.67.128'
tempdata = []

def process_packet(packet):
    if packet[IP].dst == desired_src_ip:
        cut = str(packet).split("b'")[1].split('.')[0]
        tempdata.append(cut)
        pass
        
with PcapReader(pcapng_file) as pcap_reader:
    for packet in pcap_reader:
        process_packet(packet)

my_array = np.array(tempdata)
hexWS = "".join(map(str, my_array))
with open("output.jpg",'wb') as f:
    f.write(bytes.fromhex(hexWS))
```
