<template>
  <div class="create-user-container">
    <h1>สร้างผู้ใช้ใหม่</h1>
    <p>กรุณากรอกข้อมูลเพื่อสร้างบัญชีผู้ใช้</p>
    <form v-on:submit.prevent="createUser">
      <div class="form-group">
        <input type="text" v-model="user.name" placeholder="ชื่อ" required>
      </div>
      <div class="form-group">
        <input type="text" v-model="user.lastname" placeholder="นามสกุล" required>
      </div>
      <div class="form-group">
        <input type="email" v-model="user.email" placeholder="อีเมล" required>
      </div>
      <div class="form-group">
        <input type="password" v-model="user.password" placeholder="รหัสผ่าน" required>
      </div>
      <button type="submit" class="create-btn">สร้างบัญชี</button>
    </form>
  </div>
</template>

<script>
import UsersService from '../../services/UsersService';
export default {
  data() {
    return {
      user: {
        name: '',
        lastname: '',
        email: '',
        password: '',
        status: 'active'
      }
    }
  },
  methods: {
    async createUser() {
      try {
        await UsersService.post(this.user);
        this.$router.push('/users');
      } catch (err) {
        console.log(err);
      }
    }
  }
}
</script>

<style scoped>
.create-user-container {
  padding: 40px;
  max-width: 400px;
  margin: auto;
}

.create-user-container h1 {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.create-user-container p {
  margin-bottom: 20px;
  color: #666;
  text-align: center;
}

.form-group {
  margin-bottom: 15px;
}

.form-group input {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.2);
}

.form-group input:focus {
  border-color: #ff790b;
  outline: none;
  box-shadow: 0 0 8px rgba(255, 120, 11, 0.5);
}

.create-btn {
  padding: 12px 20px;
  width: 100%;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  color: #fff;
  background-color: #ff790b;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  text-transform: uppercase;
}

.create-btn:hover {
  background-color: #e66b00;
  transform: scale(1.05);
}

.create-btn:active {
  background-color: #cc5e00;
  transform: scale(1.03);
}
</style>
