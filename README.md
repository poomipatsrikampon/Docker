# Docker
# how to use docker 
* Dockerfile คือ ไฟล์ Docker ใช้กำหนดสิ่งต่างๆที่เราต้องการในการสร้าง Image

# คำสั่งที่ใช้ในการตั้งค่า Dockerfile

* FROM เลือก base image
* RUN execute command
* CMD execute command แต่มีได้แค่ครั้งเดียวใน file        ถ้ามีมากกว่าหนึ่งจะใช้อันสุดท้าย หรือใช้เป็น default parameter ให้ ENTRYPOINT
* LABEL ใส่ metadata ให้ image
* EXPOSE กำหนดให้ container รอรับ request ตาม port ที่กำหนด ใช้คู่กับ  -p ตอนใช้ docker run
* ENV กำหนดตัวแปร environment ให้ตอนทำ image และ container
* ADD copy file เข้า image
* COPY copy file เข้า image ต่างกับ ADD ตรงที่ไฟล์ต้นฉบับได้เฉพาะ local เป็น remote url ไม่ได้
* ENTRYPOINT คำสั่งที่จะให้ run หลังจากstart container
* VOLUME กำหนด mount point ให้ image
* USER กำหนด user ที่จะใช้ run คำสั่ง RUN CMD ENTRYPOINT
* WORKDIR กำหนด working directory  สำหรับ  RUN CMD ENTRYPOINT COPY ADD
* ARG กำหนดตัวแปรไว้สำหรับตอน BUILD
* ONBUILD ใช้สำหรับ run คำสั่งแต่ให้รอ trigger เพื่อทำงานต่อในกรณีที่ต้องรอให้ build ตัวอื่นก่อน
* STOPSIGNAL สั่งให้หยุดโดยใช้ system call signal
* SHELL เปลี่ยนไปใช้ shell ที่กำหนด


# ตัวอย่างการสร้าง Dockerfile

* FROM python:3                               #กำหนด base Image
* ENV PYTHONUNBUFFERED=1                      #ตัวแปร environment
* WORKDIR /code                               #working directory
* COPY requirements.txt /code/                #copy file เข้า image
* RUN pip install -r requirements.txt         #execute command
* COPY . /code/                               #copy file เข้า image

# คำสั่งที่ใช้ในการตั้งค่า docker-compose

* version ใช้เลือก version ของ Compose file 
* services ระบุ container 
* image เรียกใช้ Image จาก Docker Hub Registry
* ports กำหนด port mapping ระหว่าง host กับ container
* volumes สร้าง volumes  2 แบบ ถ้าอยู่ภายในของ service เป็นการเชื่อมต่อกับ volume ถ้าอยู่ระดับเดียวกับ services: จะเป็นการสร้าง volume
* build ใช้ image ที่สร้างจาก Dockerfile โดยกำหนด path ไปหา Dockerfile
* links เชื่อม service เข้าด้วยกัน 
* restart: alway ให้ service นั้น restart อัตโนมัติเมื่อเกิดข้อผิดพลาด หรือทำงานอัตโนมัติเมื่อเปิดเครื่อง
* network — สร้างการสื่อสารกันระหว่าง container
* memory limit จำกัดการใช้งาน ram ที่ใช้สร้าง container
* context path ของ dockerfile ใช้ในการสร้าง container
* memory reservations กำหนดการใช้งาน ram ขั้นต่ำสำหรับ container
* depens_on ให้ service เริ่มทำงานหลังจาก service ที่ depens_on ทำงานแล้ว
