<template>
  <div class="container">
    <div class="header">
      <h1>บล็อกเกี่ยวกับการสร้างเว็บไซต์เช่า Ebook</h1>
      <p>ค้นหาข้อมูลเชิงลึก บทแนะนำ และแนวทางปฏิบัติที่ดีที่สุดสำหรับการสร้างแพลตฟอร์มเช่า Ebook ของคุณเอง</p>
    </div>

    <div class="content-section">
      <div class="content-box">
        <img src="/img/blog1.jpg" alt="บทความที่ 1" class="content-image">
        <div class="content-text">
          <h2>เริ่มต้นการสร้างแพลตฟอร์มเช่า Ebook</h2>
          <p>เรียนรู้วิธีการออกแบบและตั้งค่าแพลตฟอร์มเช่า Ebook ที่สามารถขยายและใช้งานได้ง่าย</p>
          <button class="read-more-button"><a href="#">อ่านเพิ่มเติม</a></button>
        </div>
      </div>

      <div class="content-box">
        <img src="/img/blog2.jpg" alt="บทความที่ 2" class="content-image">
        <div class="content-text">
          <h2>จัดการคลัง Ebook อย่างมีประสิทธิภาพ</h2>
          <p>ศึกษาเทคนิคในการจัดการคอลเล็กชัน Ebook หมวดหมู่ และการสร้างการมีส่วนร่วมของผู้ใช้</p>
          <button class="read-more-button"><a href="#">อ่านเพิ่มเติม</a></button>
        </div>
      </div>

      <div class="content-box">
        <img src="/img/blog3.jpg" alt="บทความที่ 3" class="content-image">
        <div class="content-text">
          <h2>สร้าง UI/UX ที่โดดเด่นสำหรับแพลตฟอร์ม Ebook</h2>
          <p>UI/UX มีความสำคัญในการรักษาผู้ใช้งาน นี่คือเคล็ดลับการออกแบบที่ช่วยให้แพลตฟอร์ม Ebook ของคุณน่าดึงดูดยิ่งขึ้น</p>
          <button class="read-more-button"><a href="#">อ่านเพิ่มเติม</a></button>
        </div>
      </div>

      <div class="content-box">
        <img src="/img/blog4.jpg" alt="บทความที่ 4" class="content-image">
        <div class="content-text">
          <h2>ปรับแต่งโมเดลการกำหนดราคาการเช่า Ebook</h2>
          <p>ค้นหาวิธีการกำหนดราคาที่เหมาะสมและแข่งขันได้ ซึ่งจะดึงดูดลูกค้ามายังแพลตฟอร์ม Ebook ของคุณมากขึ้น</p>
          <button class="read-more-button"><a href="#">อ่านเพิ่มเติม</a></button>
        </div>
      </div>
    </div>

    <footer class="footer">
      <div class="footer-content">
        <p>&copy; 2024 บล็อกการสร้างเว็บไซต์เช่า Ebook - สงวนลิขสิทธิ์</p>
        <p>ติดตามเราที่: 
          <a href="https://facebook.com" target="_blank">Facebook</a> |
          <a href="https://twitter.com" target="_blank">Twitter</a> |
          <a href="https://instagram.com" target="_blank">Instagram</a>
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.header {
  text-align: center;
  margin-bottom: 40px;
}

.header h1 {
  font-size: 2.8em;
  color: #1a237e; /* ใช้สีเข้มเพื่อสร้างความเป็นมืออาชีพ */
  margin-bottom: 10px;
  font-weight: bold;
}

.header p {
  font-size: 1.2em;
  color: #424242;
  font-style: italic;
}

.content-section {
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
  padding: 20px;
  max-width: 1400px;
  margin: auto;
}

.content-box {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin: 20px;
  width: calc(50% - 40px);
  text-align: center;
  transition: transform 0.3s ease;
  cursor: pointer;
}

.content-box:hover {
  transform: translateY(-10px);
}

.content-image {
  width: 100%;
  height: 220px;
  object-fit: cover;
  filter: grayscale(30%); /* เพิ่มเอฟเฟกต์สีเทาเล็กน้อย */
  transition: filter 0.3s ease;
}

.content-box:hover .content-image {
  filter: grayscale(0%);
}

.content-text {
  padding: 20px;
  background-color: #f0f4c3; /* ใช้สีพื้นหลังอ่อนที่ดูสบายตา */
}

.content-text h2 {
  font-size: 1.8em;
  color: #212121;
  margin-bottom: 10px;
  font-weight: bold;
}

.content-text p {
  font-size: 1em;
  color: #757575;
  margin-bottom: 20px;
}

.read-more-button {
  background-color: #ff5722; /* สีปุ่มที่สดใส */
  border: none;
  padding: 10px 20px;
  font-size: 1em;
  color: #fff;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease, transform 0.3s ease;
  text-transform: uppercase;
  font-weight: bold;
}

.read-more-button:hover {
  background-color: #e64a19;
  transform: scale(1.05);
}

.read-more-button a {
  text-decoration: none;
  color: #fff;
}


.footer {
  background-color: rgb(54, 54, 54);
  color: #fff;
  text-align: center;
  padding: 20px;
  margin-top: 40px;
  width: 100%;
}

.footer-content p {
  margin: 5px 0;
  font-size: 1em;
}

.footer-content a {
  color: #ff9100; /* สีลิงก์ใน footer */
  text-decoration: none;
  margin: 0 10px;
}

.footer-content a:hover {
  text-decoration: underline;
}
</style>
