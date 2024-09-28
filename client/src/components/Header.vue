<template>
  <div>
    <nav class="nv-navbar">
      <ul class="nav">
        <li><router-link :to="{ name: 'blogs' }">บล็อก</router-link></li>
        <li><router-link :to="{ name: 'users' }">ผู้ใช้</router-link></li>
        <li><router-link :to="{ name: 'comments' }">ความคิดเห็น</router-link></li>
        <li><router-link :to="{ name: 'login' }">เข้าสู่ระบบ</router-link></li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.nv-navbar {
  background-color: #ff790b;
  padding: 15px 0;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  width: 100%;
  z-index: 1000;
}

.nav {
  display: flex;
  justify-content: space-around;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav li {
  list-style: none;
}

.nav li a {
  color: white;
  font-weight: 600;
  text-transform: uppercase;
  text-decoration: none;
  padding: 10px 20px;
  transition: color 0.3s ease, background-color 0.3s ease;
  border-radius: 5px;
}

.nav li a:hover {
  color: #e66b00;
  background-color: rgba(255, 255, 255, 0.2);
}

.nav li a.router-link-active {
  background-color: #e66b00;
  color: white;
}

@media (max-width: 768px) {
  .nav {
    flex-direction: column;
    align-items: center;
  }

  .nav li {
    margin-bottom: 10px;
  }
}
</style>
