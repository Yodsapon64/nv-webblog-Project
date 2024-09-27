<template>
  <div class="edit-user-container">
    <h1>แก้ไขข้อมูลผู้ใช้</h1>
    <p>กรุณาแก้ไขข้อมูลที่ต้องการ</p>
    <form v-on:submit.prevent="editUser">
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
      <button type="submit" class="edit-btn">แก้ไขข้อมูล</button>
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
  async created() {
    try {
      var userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async editUser() {
      try {
        await UsersService.put(this.user);
        this.$router.push('/users');
      } catch (err) {
        console.log(err);
      }
    }
  }
}
</script>

<style scoped>
.edit-user-container {
  padding: 40px;
  max-width: 400px;
  margin: auto;
}

.edit-user-container h1 {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.edit-user-container p {
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

.edit-btn {
  padding: 12px 20px;
  width: 100%;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  color: #fff;
  background-color: #007bff;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  text-transform: uppercase;
}

.edit-btn:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}

.edit-btn:active {
  background-color: #004494;
  transform: scale(1.03);
}
</style>
