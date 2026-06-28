#  เทคโนโลยีในระดับ Application Layer (IoT Application Protocols)

## 1) ภาพรวมของ Application Layer ใน IoT

Application Layer คือชั้นที่โปรแกรมหรือบริการต่าง ๆ ใช้สื่อสารกันโดยตรง เช่น แอปบนมือถือ, ระบบ cloud, gateway, และอุปกรณ์ IoT

โดยปกติ แอปพลิเคชันบนอินเทอร์เน็ตทั่วไปจะใช้:
- **HTTP**
- **HTTPS**

ใน IoT ก็เป็นความจริงเช่นกัน แต่ IoT ต้องการโปรโตคอลที่:
- เบากว่า
- ใช้พลังงานต่ำกว่า
- ทำงานบน UDP ได้
- เหมาะกับอุปกรณ์พลังงานต่ำ
- รองรับการสื่อสารแบบ asynchronous

ดังนั้นจึงมีโปรโตคอลเฉพาะทาง เช่น CoAP, MQTT, AMQP, XMPP

#  RESTful HTTP/HTTPS และ CoAP

## 2) RESTful HTTP/HTTPS ใน IoT

แม้ IoT จะใช้ HTTP/HTTPS เช่นเดียวกับเว็บทั่วไป แต่จะใช้ในรูปแบบ:
- **RESTful API**
- **JSON payload**
- **Stateless communication**

เหมาะกับอุปกรณ์ที่ต้องการสื่อสารกับ cloud โดยตรง เช่น:
- กล้องวงจรปิด
- อุปกรณ์สมาร์ตโฮมที่มีพลังงานเพียงพอ
- Gateway ที่รวบรวมข้อมูลจากเซนเซอร์

แต่ HTTP/HTTPS ยัง “หนักเกินไป” สำหรับอุปกรณ์พลังงานต่ำ

#  CoAP (Constrained Application Protocol)

CoAP ถูกออกแบบมาเพื่อเป็น **HTTP ขนาดย่อส่วน** สำหรับอุปกรณ์ IoT พลังงานต่ำ
อ้างอิงมาตรฐาน: **RFC 7252 — Constrained Application Protocol**
คุณสมบัติหลัก:
- มีลักษณะคล้าย HTTP แต่เบากว่า
- ใช้รูปแบบ REST เช่น GET, POST, PUT, DELETE
- ทำงานบน **UDP** (ไม่ใช่ TCP)
- ใช้ร่วมกับ **6LoWPAN** ได้ดี
- เหมาะกับอุปกรณ์ที่มีพลังงานต่ำและ bandwidth ต่ำ
- รองรับ multicast
- มีระบบ reliability แบบ lightweight

CoAP ถูกใช้ใน:
- เซนเซอร์พลังงานต่ำ
- ระบบ home automation
- ระบบ smart building
- อุปกรณ์ที่ใช้ 6LoWPAN หรือ Thread

#  MQTT (Message Queuing Telemetry Transport)

MQTT เป็นโปรโตคอลที่ได้รับความนิยมสูงที่สุดในโลก IoT
คุณสมบัติหลัก:
- ใช้รูปแบบ **publish/subscribe**
- ใช้พลังงานต่ำมาก
- ใช้ bandwidth ต่ำ
- ทำงานบน TCP
- มี broker เป็นตัวกลาง (เช่น Mosquitto, EMQX, HiveMQ)
- เหมาะกับอุปกรณ์ที่ส่งข้อมูลเป็นช่วง ๆ (telemetry)

MQTT เหมาะกับ:
- เซนเซอร์เกษตร
- ระบบบ้านอัจฉริยะ
- ระบบโรงงาน
- ระบบติดตามทรัพย์สิน
- ระบบที่ต้องการ real-time แบบเบา

MQTT คือ “ภาษากลาง” ของ IoT ในหลายแพลตฟอร์ม เช่น AWS IoT, Azure IoT Hub, Google IoT Core

#  AMQP (Advanced Message Queuing Protocol)

AMQP เป็นโปรโตคอลที่ออกแบบมาสำหรับระบบ enterprise messaging

คุณสมบัติ:
- ทำงานบน TCP
- มีความน่าเชื่อถือสูง
- รองรับ queue, routing, topic, exchange
- ใช้ในระบบที่ต้องการความเสถียรสูง
- เหมาะกับระบบ IoT ที่ต้องการประมวลผลข้อมูลจำนวนมากในฝั่ง cloud

นิยมใช้ใน:
- ระบบอุตสาหกรรม
- ระบบ enterprise IoT
- ระบบที่ต้องการ message broker ระดับองค์กร (เช่น RabbitMQ)

#  XMPP (Extensible Messaging and Presence Protocol)

XMPP เดิมเป็นโปรโตคอลสำหรับ instant messaging แต่ถูกนำมาใช้ใน IoT เพราะ:
- รองรับการสื่อสารแบบ real-time
- รองรับการเข้ารหัส
- รองรับการขยายฟังก์ชัน (extensible)
- ทำงานบน TCP
- เหมาะกับระบบที่ต้องการการสื่อสารแบบสองทาง (bidirectional)

ใช้ใน:
- ระบบควบคุมอุปกรณ์แบบ real-time
- ระบบที่ต้องการ presence (สถานะออนไลน์/ออฟไลน์)
- ระบบที่ต้องการข้อความแบบทันที

#  สรุป Application Layer Technologies สำหรับ IoT

| โปรโตคอล       | ลักษณะเด่น                | เหมาะกับ                            |
| -------------- | ------------------------- | ----------------------------------- |
| **HTTP/HTTPS** | มาตรฐานเว็บทั่วไป         | อุปกรณ์ที่พลังงานเพียงพอ, gateway   |
| **CoAP**       | HTTP แบบย่อส่วนบน UDP     | 6LoWPAN, Thread, เซนเซอร์พลังงานต่ำ |
| **MQTT**       | publish/subscribe, เบามาก | telemetry, smart home, agriculture  |
| **AMQP**       | enterprise messaging      | cloud IoT, industrial IoT           |
| **XMPP**       | real-time messaging       | bidirectional IoT communication     |

Application Layer คือชั้นที่ทำให้ IoT “พูดคุยกับระบบจริง” เช่น cloud, mobile app, dashboard และบริการต่าง ๆ

----

#  MQTT (Message Queue Telemetry Transport)

![](Images/MQTT.png)
## 1) แนวคิดหลักของ MQTT

MQTT เป็นโปรโตคอลสื่อสารแบบ **publish/subscribe-based messaging** ที่ออกแบบมาเพื่อรองรับอุปกรณ์ IoT พลังงานต่ำและเครือข่ายที่มีความเสถียรต่ำ โดยเน้นให้:
- ใช้ **bandwidth ต่ำมาก**
- ใช้ **พลังงานต่ำมาก**
- ทำงานได้ดีบนเครือข่ายที่มี **packet loss สูง**
- รองรับการเชื่อมต่อที่ **ไม่เสถียร** (unstable connectivity)
- ส่งข้อมูลแบบ **telemetry** (ข้อมูลสถานะเป็นช่วง ๆ)

MQTT จึงกลายเป็นโปรโตคอลที่ได้รับความนิยมสูงที่สุดในโลก IoT

## 2) Publish/Subscribe Model

MQTT ใช้รูปแบบการสื่อสารแบบ **publish/subscribe** โดยมีตัวกลางเรียกว่า **broker**

### โครงสร้างพื้นฐานของ MQTT:
- **Publisher** → อุปกรณ์ที่ส่งข้อมูล
- **Subscriber** → อุปกรณ์/ระบบที่ต้องการรับข้อมูล
- **Broker** → ตัวกลางที่รับข้อมูลจาก publisher และกระจายให้ subscriber

ข้อดีของรูปแบบนี้:
- อุปกรณ์ไม่ต้องรู้จักกันโดยตรง
- ลดภาระการเชื่อมต่อแบบ point-to-point
- รองรับอุปกรณ์จำนวนมาก
- เหมาะกับระบบที่ต้องการ real-time แบบเบา

## 3) เหตุผลที่ MQTT เหมาะกับ IoT

MQTT ถูกออกแบบมาเพื่อใช้งานในสภาพแวดล้อมที่มีข้อจำกัด เช่น:
- เครือข่าย cellular ที่สัญญาณไม่เสถียร
- เครือข่าย LPWAN ที่ bandwidth ต่ำ
- อุปกรณ์ที่ต้องประหยัดพลังงาน
- อุปกรณ์ที่ส่งข้อมูลเป็นช่วง ๆ (bursts)
- อุปกรณ์ที่หลับ/ตื่นเป็นระยะ (sleep cycles)

MQTT จึงเหมาะกับ:
- เซนเซอร์เกษตร
- ระบบบ้านอัจฉริยะ
- ระบบติดตามทรัพย์สิน
- ระบบโรงงาน
- ระบบที่ต้องการส่งข้อมูลสถานะอย่างต่อเนื่องแต่เบามาก

## 4) ความสามารถสำคัญของ MQTT

### **1) ใช้ bandwidth ต่ำมาก**

MQTT มี overhead น้อยกว่า HTTP/HTTPS อย่างมหาศาล เหมาะกับเครือข่ายที่มีความเร็วต่ำ เช่น NB‑IoT, LTE‑M

### **2) ทำงานได้ดีบนเครือข่ายที่ไม่เสถียร**

MQTT ถูกออกแบบมาให้ทนต่อ:
- การเชื่อมต่อหลุดบ่อย
- packet loss
- latency สูง
- jitter สูง

### **3) QoS (Quality of Service)**

MQTT มีระดับ QoS ให้เลือกตามความต้องการ:
- **QoS 0** → ส่งแบบไม่รับประกัน
- **QoS 1** → ส่งอย่างน้อยหนึ่งครั้ง
- **QoS 2** → ส่งอย่างแน่นอนหนึ่งครั้ง (ปลอดภัยที่สุด)

### **4) Lightweight**

เหมาะกับไมโครคอนโทรลเลอร์ เช่น:
- ESP32
- ESP8266
- STM32
- Arduino
- Raspberry Pi Pico

## 5) การใช้งาน MQTT ในโลกจริง

MQTT ถูกใช้ในแพลตฟอร์ม IoT ชั้นนำ เช่น:
- AWS IoT Core
- Azure IoT Hub
- Google Cloud IoT
- HiveMQ
- EMQX
- Mosquitto (open-source broker)

ใช้ในงาน:
- Smart home
- Smart agriculture
- Smart factory
- Smart city
- Telemetry systems
- ระบบแจ้งเตือน real-time

MQTT คือ “ภาษากลาง” ของ IoT ในหลายระบบทั่วโลก

# สรุป MQTT

MQTT เป็นโปรโตคอล publish/subscribe ที่ออกแบบมาเพื่อใช้งานในระบบที่มี bandwidth ต่ำและการเชื่อมต่อไม่เสถียร เหมาะกับอุปกรณ์ IoT พลังงานต่ำที่ต้องส่งข้อมูลสถานะเป็นช่วง ๆ

| คุณสมบัติ  | รายละเอียด                                  |
| ---------- | ------------------------------------------- |
| รูปแบบ     | Publish/Subscribe                           |
| ตัวกลาง    | Broker                                      |
| Bandwidth  | ต่ำมาก                                      |
| ความเสถียร | ทนต่อการเชื่อมต่อไม่เสถียร                  |
| QoS        | 0, 1, 2                                     |
| เหมาะกับ   | Telemetry, smart home, agriculture, factory |

------

#  AMQP (Advanced Message Queuing Protocol)

![](Images/AMQP.png)

## 1) แนวคิดหลักของ AMQP

AMQP เป็น **open standard messaging protocol** ที่ออกแบบมาเพื่อใช้งานกับระบบ **message-oriented middleware** ซึ่งเป็นระบบที่ใช้ “ข้อความ (messages)” เป็นตัวกลางในการสื่อสารระหว่างบริการหรืออุปกรณ์ต่าง ๆ

คุณสมบัติหลักของ AMQP:
- เป็น **open standard**
- รองรับการสื่อสารแบบ **message-oriented middleware**
- มีความน่าเชื่อถือสูง (high reliability)
- รองรับการจัดการข้อความแบบซับซ้อน เช่น queue, routing, exchange
- เหมาะกับระบบ enterprise และระบบ IoT ที่ต้องการความเสถียรสูง

## 2) AMQP และ RabbitMQ

AMQP ได้รับการพัฒนาและผลักดันโดย **RabbitMQ** ซึ่งเป็นหนึ่งใน message broker ที่ได้รับความนิยมสูงที่สุดในโลก

RabbitMQ ทำให้ AMQP กลายเป็นมาตรฐานในงาน:
- ระบบ enterprise messaging
- ระบบ microservices
- ระบบ IoT ที่ต้องการความเสถียรสูง
- ระบบที่ต้องการการจัดการข้อความจำนวนมาก
- ระบบที่ต้องการ routing แบบซับซ้อน

RabbitMQ รองรับ:
- AMQP
- MQTT
- STOMP
- และโปรโตคอลอื่น ๆ ผ่าน plugin

แต่ AMQP คือโปรโตคอลหลักที่ RabbitMQ ใช้ในการจัดการข้อความแบบเต็มรูปแบบ

## 3) AMQP แตกต่างจาก MQTT อย่างไร

แม้ AMQP และ MQTT จะเป็นโปรโตคอล messaging เหมือนกัน แต่มีจุดประสงค์ต่างกัน:

| โปรโตคอล | จุดเด่น                                      | เหมาะกับ                             |
| -------- | -------------------------------------------- | ------------------------------------ |
| **MQTT** | เบามาก, bandwidth ต่ำ, publish/subscribe     | อุปกรณ์ IoT พลังงานต่ำ               |
| **AMQP** | เสถียรสูง, enterprise-grade, queue + routing | ระบบองค์กร, cloud IoT, microservices |

MQTT เหมาะกับอุปกรณ์ IoT ที่ส่งข้อมูล telemetry AMQP เหมาะกับระบบ backend ที่ต้องการความเสถียรและการจัดการข้อความจำนวนมาก

## 4) ความสามารถสำคัญของ AMQP

AMQP มีฟีเจอร์ที่ MQTT ไม่มี เช่น:

### **1) Message Queueing**

รองรับการจัดคิวข้อความอย่างเป็นระบบ

### **2) Routing แบบซับซ้อน**

ใช้ “exchange” เพื่อกำหนดวิธีส่งข้อความ เช่น:

- direct exchange
- topic exchange
- fanout exchange
- headers exchange

### **3) Reliability สูงมาก**

รองรับ:
- message acknowledgment
- durable queues
- persistent messages
- transaction-like behavior

### **4) ทำงานบน TCP**

เหมาะกับระบบที่ต้องการความเสถียรสูงและ latency ต่ำ

## 5) การใช้งาน AMQP ในโลกจริง

AMQP นิยมใช้ใน:
- ระบบ enterprise IoT
- ระบบอุตสาหกรรม (Industrial IoT)
- ระบบ cloud backend
- ระบบ microservices
- ระบบที่ต้องการ message broker ระดับองค์กร
- ระบบที่ต้องการ routing แบบซับซ้อน
- ระบบที่ต้องการความน่าเชื่อถือสูงมาก

แพลตฟอร์มที่ใช้ AMQP:
- RabbitMQ
- Azure Service Bus
- Apache Qpid
- Red Hat AMQ

#  สรุป AMQP

AMQP เป็นโปรโตคอล messaging แบบ open standard ที่ออกแบบมาเพื่อระบบ enterprise และระบบ IoT ที่ต้องการความเสถียรสูง โดยใช้ร่วมกับ message-oriented middleware เช่น RabbitMQ

| คุณสมบัติ | รายละเอียด                                         |
| --------- | -------------------------------------------------- |
| ประเภท    | Open standard messaging                            |
| รูปแบบ    | Message-oriented middleware                        |
| พัฒนาโดย  | RabbitMQ (ผลักดันมาตรฐาน)                          |
| จุดเด่น   | Reliability สูง, routing ซับซ้อน, queue management |
| เหมาะกับ  | Enterprise IoT, cloud backend, microservices       |

----------

#  XMPP (Extensible Messaging and Presence Protocol)

## 1) จุดกำเนิดของ XMPP

XMPP ถูกออกแบบมาในยุคแรกเพื่อรองรับ **real-time human-to-human communication** เช่น:
- แชต (instant messaging)
- ระบบ presence (ออนไลน์/ออฟไลน์)
- การส่งข้อความแบบทันที
- การสื่อสารแบบสองทาง (bidirectional)

จุดเด่นคือความสามารถในการสื่อสารแบบ **real-time** และการจัดการสถานะของผู้ใช้งาน (presence) ซึ่งเป็นสิ่งที่โปรโตคอลอื่นในยุคนั้นทำได้ไม่ดี

## 2) จาก human-to-human → machine-to-machine (M2M)

เมื่อ IoT เริ่มเติบโต นักพัฒนาพบว่า:
- XMPP รองรับ real-time
- XMPP รองรับการสื่อสารแบบสองทาง
- XMPP รองรับการเข้ารหัส
- XMPP รองรับการขยายฟังก์ชัน (extensible)
- XMPP มีระบบ presence ที่เหมาะกับการตรวจสถานะอุปกรณ์

จึงมีการนำ XMPP มาปรับใช้กับ **machine-to-machine (M2M) communication** โดยตรง

ตัวอย่างการใช้งาน:
- อุปกรณ์แจ้งสถานะออนไลน์/ออฟไลน์
- อุปกรณ์ส่งข้อมูลแบบ real-time
- ระบบควบคุมอุปกรณ์อัจฉริยะ
- ระบบที่ต้องการสื่อสารแบบสองทางทันที เช่น smart appliances

## 3) วัตถุประสงค์หลัก: ส่งผ่าน XML data

XMPP ใช้ **XML** เป็นรูปแบบข้อมูลหลักในการสื่อสาร
ข้อดีของ XML ใน XMPP:
- อ่านง่าย
- ขยายโครงสร้างได้ (extensible)
- รองรับ metadata
- เหมาะกับการส่งข้อความที่มีโครงสร้าง
- เหมาะกับการสื่อสารแบบ real-time ที่ต้องการความยืดหยุ่น

แม้ XML จะ “หนักกว่า” JSON แต่ในระบบที่ต้องการความยืดหยุ่นและการกำหนดโครงสร้างข้อความที่ชัดเจน XML ยังมีข้อได้เปรียบ

## 4) ทำไม XMPP เหมาะกับเครื่องใช้อัจฉริยะ (Smart Appliances)

เครื่องใช้อัจฉริยะ เช่น:
- Smart fridge
- Smart washing machine
- Smart air conditioner
- Smart lighting
- Smart speakers

ต้องการคุณสมบัติ:
- การสื่อสารแบบสองทาง (bidirectional)
- การแจ้งสถานะ real-time
- การควบคุมแบบทันที
- การจัดการสถานะออนไลน์/ออฟไลน์
- การส่งข้อมูลแบบมีโครงสร้าง

XMPP รองรับทั้งหมดนี้โดยกำเนิด

จึงถูกนำมาใช้ในระบบ smart home และ smart appliances อย่างแพร่หลาย

## 5) เปรียบเทียบ XMPP กับ MQTT และ AMQP

| โปรโตคอล | จุดเด่น                            | เหมาะกับ                            |
| -------- | ---------------------------------- | ----------------------------------- |
| **MQTT** | เบามาก, publish/subscribe          | เซนเซอร์พลังงานต่ำ                  |
| **AMQP** | enterprise messaging, queue        | cloud backend, microservices        |
| **XMPP** | real-time, bidirectional, presence | smart appliances, real-time control |

XMPP ไม่ได้เบาเท่า MQTT และไม่ซับซ้อนเท่า AMQP แต่โดดเด่นด้าน **real-time + presence + bidirectional communication**





