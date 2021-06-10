# Docker
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

* FROM python:3                               
* ENV PYTHONUNBUFFERED=1                     
* WORKDIR /code                               
* COPY requirements.txt /code/                
* RUN pip install -r requirements.txt        
* COPY . /code/                               

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

# ตัวอย่างการสร้าง docker-compose.yml

* version: "3.9"
   
* services:
*  db:
*    image: postgres
*    environment:
*      - POSTGRES_DB=postgres
*      - POSTGRES_USER=postgres
*      - POSTGRES_PASSWORD=postgres
*  web:
*    build: .
*    command: python manage.py runserver 0.0.0.0:8000
*    volumes:
*      - .:/code
*    ports:
*      - "8000:8000"
*    depends_on:
*      - db

# ทดลองสร้าง Image
* สร้างไฟล์
* -Dockerfile
* -docker-compose.yml
* -requirements.txt
* sudo docker-compose run web django-admin startproject composeexample . #สร้าง django project
* เปลี่ยน db ของ django

* 'ENGINE': 'django.db.backends.postgresql',
*        'NAME': 'postgres',
*        'USER': 'postgres',
*        'PASSWORD': 'postgres',
*        'HOST': 'db',
*        'PORT': 5432,

* docker-compose up #run docker-compose

# requirements.txt
* Django>=3.0,<4.0
* psycopg2-binary>=2.8
* djangorestframework>=3.12.2

