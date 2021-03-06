![](https://hidden-process.com/app/uploads/2019/10/security-misconfiguration.png)

# ช่องโหว่ประเภท Security Misconfiguration

`Security Misconfiguration` เป็นช่องโหว่ที่ถูกจัดให้อยู่ในลำดับที่ 5 ของ OWASP TOP 10 2013 ช่องโหว่ประเภทนี้เป็นช่องโหว่ที่เกิดจากการตั้งค่าที่ผิดพลาดของระบบ เนื่องจากเว็บแอปพลิเคชันประกอบไปด้วยหลายส่วนประกอบ ทุกส่วนต้องได้รับการดูและและตั้งค่าอย่างถูกต้องมิฉะนั้นก็จะกลายเป็นช่องโหว่ที่นำความเสียหายมาสู่ระบบทั้งระบบ ในบทความนี้จะอธิบายตัวอย่างช่องโหว่ประเภทนี้และผลกระทบที่อาจจะเกิดขึ้นต่อระบบ

### อะไรที่สามารถทำให้เกิดช่องโหว่ Security Misconfiguration ได้บ้าง?

ความมั่นคงปลอดภัยของเว็บแอปพลิเคชันนั้นขึ้นอยู่กับส่วนประกอบทุกส่วน อย่างไรก็ตามส่วนประกอบในฝังของผู้ใช้งาน (client-side) นั้น อยู่นอกเหนือความควบคุมของผู้พัฒนาระบบ ดังนั้น ในบทความนี้จะขอมุ่งเน้นไปที่ส่วนประกอบของเว็บแอปพลิเคชันในฝั่งเซิร์ฟเวอร์ ซึ่งปะกอบไปด้วย

### Web application

ช่องโหว่สามารถเกิดขึ้นได้จากการตั้งค่าที่ผิดพลาดของเว็บแอปพลิเคชัน เช่น การกำหนดสิทธิ์ในการเข้าถึงแต่ละส่วนอย่างผิดพลาด ช่องโหว่ประเภทนี้ไม่ได้รวมถึงการทำ authorization ที่ผิดพลาด แต่หมายถึงการตั้งค่าสิทธิ์ หรือ การตั้งค่าอื่น ๆ ที่ผิดพลาด นอกจากนี้หากเว็บแอปพลิเคชันมีการใช้ Content Management System (Joomla, WordPress, Dupal) เป็นโครงสร้างและไม่ได้ทำการ update security patch ให้กับ CMS เหล่านี้ก็ถูกจัดให้เป็นช่องโหว่ในประเภท Security Misconfiguration โดยผลกระทบของช่องโหว่ก็แตกต่างกันไป เช่น การตั้งค่าที่ผิดพลาดอาจจะนำไปสู่การเปิดเผยข้อมูลความลับให้กับผู้ใช้งานที่ไม่สมควร การอนุญาตให้ผู้ใช้งานลบข้อมูลสำคัญบางอย่างของระบบเป็นต้น

### Web application framework

Web application framework เช่น Hibernate, CakePHP, หรือ Django ได้รับความนิยมในการนำมาช่วยในการพัฒนาเว็บแอปพลิเคชันมากขึ้น เนื่องจากช่วยให้ผู้พัฒนาสามารถพัฒนาเว็บแอปพลิเคชันได้รวดเร็วและเป็นระเบียบขึ้น อย่างไรก็ตาม เนื่องจาก web application framework ก็เป็น software ตัวหนึ่งซึ่งสามารถมีช่องโหว่ได้เช่นกันซึ่งหากไม่ได้รับการ update security patch เป็นเวลานานก็สามารถเป็นช่องทางในการโจมตีสำหรับผู้ไม่หวังดีได้

### Web server software

Web server software เช่น Apache, WebSphere, NodeJS เป็นส่วนประกอบของการทำงานของเว็บแอปพลิเคชัน หน้าที่ของ web server software คือการรับ HTTP request มาประมวลผล ดังนั้น เรียกได้ว่า web server software เป็นส่วนประกอบที่มีการรับข้อมูลจากผู้ใช้งานโดยตรง configuration การทำงานของ interpreter และ compliler ที่ใช้ในเว็บแอปพลิเคชัน รวมถึง การตั้งค่าการอื่น ๆ เกี่ยวกับการจัดการ HTTP requeset และ HTTP response ต่างอยู่ที่ web server software configuration ดังนั้น ช่องโหว่ที่เกิดจากการตั้งค่า web server software สามารถสร้างความเสียหายได้กับเว็บแอปพลิเคชันได้อย่างมาก ตัวอย่างของ security misconfiguration ใน web server software ที่ได้เจอได้บ่อยเช่น

1. การเปิด directory listing
2. ไม่ได้ update security patch เป็นเวลานาน
3. ตั้งค่า session ไม่ถูกต้องทำให้เกิด session fixation
4. ไม่ได้ตั้งค่า HttpOnly ให้กับ Cookie
5. เรียกใช้งานเวอร์ชันของ interpreter และ complier เช่น PHP/JAVA/ASP/Python ที่มีช่องโหว่
6. Error message ที่บอกให้ผู้ใช้งานได้ทราบถึงข้อมูลของซอร์ฟแวร์ที่ใช้ในเครื่องเซิร์ฟเวอร์

ตัวอย่าง directory listing เปิดโอกาสให้ผู้ใช้งานเห็นไฟล์ทั้งหมดใน directory

![](https://i2.wp.com/blog.tamacorp.co/wp-content/uploads/2016/01/Screen-Shot-2559-01-18-at-1.01.31-PM.png?w=421&ssl=1)

### Database

ฐานข้อมูลอาจจะเป็นสิ่งที่มีค่าที่สุดของเว็บแอปพลิเคชันจึงทำให้ฐานข้อมูลตกเป็นเป้าหมายหลักของผู้ไม่หวังดี ทำให้ช่องโหว่ที่เกิดขึ้นกับฐานข้อมูลนั้นสร้างความเสียหายต่อระบบได้อย่างรุนแรง การตั้งค่าฐานข้อมูลที่ผิดพลาดที่พบบ่อยได้แก่

1. การลืมที่จะปิด default user
2. การตั้งสิทธิ์ในการเข้าถึงฐานข้อมูลไม่รัดกุม เช่น การใช้ root user ในการเข้าถึงฐานข้อมูล
3. ไม่ได้ update security patch

### Operating System

`OS` เป็นอีกหนึ่งส่วนประกอบสำคัญของระบบเว็บแอปพลิเคชัน ช่องโหว่หรือการตั้งค่าที่ผิดพลาดของ OS สามารถนำไปสู่การเข้าควบคุมทั้ง ฐานข้อมูล ซอร์สโค้ด และ เครื่องเซิร์ฟเวอร์ ช่องโหว่ที่บนได้บน OS ส่วนใหญ่จะเป็นช่องโหว่เกี่ยวกับ system ซึ่งเกิดจาก ไม่ได้ทำการ update security patch หรือ OS เป็นเวอร์ชันเก่าที่ผู้ผลิตไม่รองรับแล้ว นอกจากนี้ การที่เซิร์ฟเวอร์ให้บริการหลาย service บนเครื่องเดียวกันส่งผลให้เกิดโอกาสที่จะเกิดช่องโหว่ได้มากขึ้น การเปิด service ที่ไม่ได้ใช้งานบน OS นั้นเปรียบเสมือนการเพิ่มโอกาสให้เซิร์ฟเวอร์มีช่องทางในการโจมตีมากยิ่งขึ้น

### แนวทางการป้องกัน Security Misconfiguration

Security Misconfiguration เกิดจากการผิดพลาดในการตั้งค่าของส่วนประกอบต่าง ๆ การตั้งค่าที่เหมาะสมขึ้นอยู่กับแต่ละเทคโนโลยีที่ถูกนำมาใช้งาน แนวทางการป้องกัน security misconfiguration จึงมีรูปแบบที่แตกต่างและหลายหลายขึ้นอยู่กับเทคโนโลยี อย่างไรก็ตาม ลักษณะของช่องโหว่ต่าง ๆ ที่เกิดขึ้นนั้นก็มีความคล้ายกัน การทำ check list เพื่อใช้ในการตรวจสอบช่องโหว่นั้นก็จะเป็นสิ่งที่ดี ข้อแนะนำเกี่ยวกับการตรวจสอบ security misconfiguration อาจจะสรุปได้โดยสังเขปดังนี้

1. ตรวจสอบ security patch ของส่วนประกอบต่าง ๆของเว็ปแอปพลิเคชันให้ดี ตัวอย่างเช่น หากใช้ WordPress เป็น CMS ให้กับเว็บแอปพลิเคชันผู้ดูแลก็ควรที่จะเข้าไปดู security patch update ของ WordPress ที่ https://wordpress.org/news/category/security/ และคอย update security patch ที่อาจส่งผลกระทบต่อความมั่นคงปลอดภัยของเว็บแอปพลิเคชัน

2. ปิดการใช้งาน default user ของทุกส่วนประกอบของเว็บแอปพลิเคชัน default user จะตกเป็นเป้าหมายหลักของผู้ไม่หวังดี หากผู้ดูแลระบบลืมที่จะเปลี่ยน password ของ default user ก็เหมือนเป็นการเปิดประตูบ้านให้ใครก็ได้สามารถเข้ามาในระบบ ดังนั้น เพื่อเป็นการป้องกันความผิดพลาดนี้ การปิด default user ของทุกส่วนประกอบ OS Database Web Application จะเป็นการปิดโอกาสช่องโหว่ประเภทนี้

3. ปิด error message ทั้งหมด หรือทำการเปลี่ยน error message ให้อยู่ในรูปแบบที่ผู้ดูแลระบบคนเดียวเท่านั้นที่เข้าใจ error message เปิดโอกาสให้ผู้ไม่หวังดีเรียนรู้เกี่ยวกับส่วนประกอบและเวอร์ชัน ซึ่งข้อมูลเหล่านี้ทำให้ง่ายแก่การหาช่องโหว่และแนวทางในการโจมตี

ตัวอย่าง error message ที่ดีของ youtube.com

![](https://i2.wp.com/blog.tamacorp.co/wp-content/uploads/2016/01/Screen-Shot-2559-01-18-at-12.55.11-PM.png?w=707&ssl=1)

ตัวอย่าง error message ที่บอกเวอร์ชันและ OS ที่ใช้งาน เปิดการเปิดเผยข้อมูลโดยไม่จำเป็น

![](https://i2.wp.com/blog.tamacorp.co/wp-content/uploads/2016/01/Screen-Shot-2559-01-18-at-12.57.49-PM.png?w=458&ssl=1)

4. การทำ configuration review ทุก ๆ ไตรมาสหรือบ่อยที่สุดเท่าที่จะทำได้ เพื่อให้มั่นใจว่าการตั้งค่าต่าง ๆ ไม่มีข้อผิดพลาด

5. least privilege คือการให้สิทธิ์ให้น้อยที่สุดเท่าที่เป็นไปได้ ตัวอย่างเช่น หากเว็ปแอพลิเคชันมีการใช้ฐานข้อมูลเพียง 1 table ก็ควรสร้าง user account ในฐานข้อมูลให้สามารถเข้าถึงได้เพียง 1 table เท่านั้น เพื่อป้องกันกรณีที่ user account รั่วไหลเป็นต้น

### สรุป

ช่องโหว่ประเภท security misconfiguration เป็นช่องโหว่ที่เกิดขึ้นได้ง่ายและบ่อย เนื่องจากเว็บแอปพลิเคชันมีความซับซ้อนและมีส่วนประกอบในการทำงานมากยิ่งขึ้น ช่องโหว่ในส่วนใดส่วนหนึ่งอาจจะนำไปสู่ความเสียหายของทั้งระบบ แนวทางในการป้องกัน security misconfiguration นั้นมีความหลากหลาย การทำ checklist เพื่อตรวจสอบเป็นแนวทางหนึ่งที่สามารถลดจำนวนช่องโหว่ประเภทนี้ลงได้

#### References:

- https://blog.tamacorp.co/ช่องโหว่ประเภท-security-misconfiguration/


