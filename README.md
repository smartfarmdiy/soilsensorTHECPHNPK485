# soilsensorTHECPHNPK485
How-to-configure-code-arduino-max485-soilsensorTHECPHNPK485

*** สิ่งที่ต้องดูจากคู่มือเซนเซอร์  ****

จาก “คู่มือ config” ให้หาข้อมูลประมาณนี้ (มักจะมีในหัวข้อ Modbus / RS485 / Register Table):

Modbus Address (Slave ID)

เช่น 1, 2, 10 … มักเขียนว่า “Device Address”, “Slave ID”

Serial Setting

Baudrate: เช่น 4800 / 9600 / 19200

Data bits / Parity / Stop bits: เช่น 8N1 (8 data, No parity, 1 stop)

Register Mapping
ดูตารางประมาณนี้ในคู่มือ (ชื่ออาจต่างกัน):

N value -> Register Address = ?

P value -> Register Address = ?

K value -> Register Address = ?

บางรุ่นอาจเก็บเป็น block: เช่น start 0x0001 ยาว 3 register

หรือ N,P,K ปนกับ Temp / Moisture / EC ใน block ยาว (ก็อ่านทีเดียวหลายช่องได้)

Data Type / Scaling

บางรุ่นบอกว่า ค่าใน register ต้อง /10 หรือ /100 เพื่อให้ได้ค่าจริง เช่น 123 → 12.3


“กรอกอะไร” จากคู่มือลงโค้ด

ตั้งค่า ID เซนเซอร์

ดูในคู่มือว่า Default Address เท่าไหร่

แทนใน SLAVE_ID

ดู Register Address

หาตารางที่เขียนประมาณ

Nitrogen value register: 0x0001

Phosphorus value register: 0x0002

Potassium value register: 0x0003

เลือก Address ตัวแรกเป็น REG_START

นับจำนวนช่องที่จะอ่านเป็น REG_NUM

Scaling

ถ้าในคู่มือเขียนว่า “Actual value = Register / 10”
เปลี่ยนตรงนี้:

float N = regs[0] / 10.0;
float P = regs[1] / 10.0;
float K = regs[2] / 10.0;



****Serial Setting*****

ตั้ง Serial2.begin(baud, mode, RXD2, TXD2); ให้ตรงกับคู่มือ
