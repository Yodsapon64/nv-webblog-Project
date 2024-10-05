<template>
  <div class="create-user-container">
    <div class="create-card">
      <div class="create-left">
        <img src="@/assets/dragon ball.jpg" alt="Create User Image"> <!-- เพิ่มเส้นทางรูปภาพ -->
      </div>
      <div class="create-right">
        <h1>สร้างผู้ใช้ใหม่</h1>
        <p>กรุณากรอกข้อมูลเพื่อสร้างบัญชีผู้ใช้</p>
        <form v-on:submit.prevent="createUser">
          <div class="form-group">
            <input type="text" v-model="user.name" placeholder="ชื่อ" required @focus="showTooltip('กรุณากรอกชื่อ')" @blur="hideTooltip" />
            <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
          </div>
          <div class="form-group">
            <input type="text" v-model="user.lastname" placeholder="นามสกุล" required @focus="showTooltip('กรุณากรอกนามสกุล')" @blur="hideTooltip" />
            <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
          </div>
          <div class="form-group">
            <input type="email" v-model="user.email" placeholder="อีเมล" required @focus="showTooltip('กรุณากรอกอีเมลที่ถูกต้อง')" @blur="hideTooltip" />
            <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
          </div>
          <div class="form-group">
            <input type="password" v-model="user.password" placeholder="รหัสผ่าน" required @focus="showTooltip('ตั้งรหัสผ่านที่ปลอดภัย')" @blur="hideTooltip" />
            <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
          </div>
          <button type="submit" class="create-btn">สร้างบัญชี</button>
        </form>
      </div>
    </div>
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
      },
      tooltipVisible: false,
      tooltipText: ''
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
    },
    showTooltip(text) {
      this.tooltipVisible = true;
      this.tooltipText = text;
    },
    hideTooltip() {
      this.tooltipVisible = false;
      this.tooltipText = '';
    }
  }
}
</script>

<style scoped>
.create-user-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.create-card {
  background-color: #d8d8d8;
  box-shadow: 0 4px 8px rgba(255, 116, 3, 0.1);
  border-radius: 10px;
  overflow: hidden;
  display: flex;
  max-width: 800px;
  width: 100%;
}

.create-left {
  flex: 1;
  position: relative;
}

.create-left img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.create-right {
  padding: 40px;
  flex: 1;
}

.create-right h1 {
  margin-bottom: 20px;
  font-size: 24px;
  color: #333;
}

.create-right p {
  margin-bottom: 20px;
  color: #666;
}

.form-group {
  margin-bottom: 20px;
  position: relative;
}

.form-group input {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.form-group input:focus {
  border-color: #ff790b;
  box-shadow: 0 0 8px rgba(255, 116, 3, 0.3);
  outline: none;
}

.tooltip {
  position: absolute;
  top: -5px;
  right: 10px;
  background-color: #e0e0e0;
  color: #555;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 12px;
  opacity: 0.9;
}

.create-btn {
  padding: 12px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s ease, transform 0.3s ease;
  width: 100%;
  background-color: #ff790b;
  color: #fff;
}

.create-btn:hover {
  background-color: #e66b00;
  transform: scale(1.05);
}
</style>
