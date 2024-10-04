<template>
  <div class="topbar">
    <div class="logo">
      <router-link :to="{ name: 'home' }">เว็บแอปพลิเคชั่นสำหรับการเช่าหนังสือ Ebook</router-link>
    </div>
    <ul class="menu">
      <li><router-link :to="{ name: 'blogs' }">หน้าแรก</router-link></li>
      <li><router-link :to="{ name: 'users' }">ข้อมูลผู้ใช้</router-link></li>
      <li><router-link :to="{ name: 'user-create' }">สร้างบัญชีผู้ใช้งาน</router-link></li>
      <li><router-link :to="{ name: 'comments' }">ความคิดเห็น</router-link></li>
      <li><router-link :to="{ name: 'login' }">เข้าสู่ระบบ</router-link></li>
    </ul>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background-color: rgb(54, 54, 54); /* สีพื้นหลัง */
  margin: 8px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* เงา */
  height: 60px;
}

.logo a {
  text-decoration: none;
  font-size: 18px;
  font-weight: bold;
  color: #fff; /* สีตัวอักษรโลโก้ */
}

.menu {
  display: flex;
  align-items: center;
  list-style: none;
  margin: 0;
}

.menu li {
  margin-left: 15px;
}

.menu li a {
  text-decoration: none;
  color: #fff; /* สีตัวอักษรในเมนู */
  font-weight: bold;
  transition: color 0.3s ease; /* การเปลี่ยนสี */
}

.menu li a:hover {
  color: #ff790b; /* สีเมื่อเมาส์อยู่เหนือเมนู */
}

@media (max-width: 768px) {
  .menu {
    flex-direction: column;
    align-items: center;
  }

  .menu li {
    margin-bottom: 10px;
  }
}
</style>
