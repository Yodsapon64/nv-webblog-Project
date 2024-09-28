<template>
  <div class="edit-user-container">
    <h1>แก้ไขข้อมูลผู้ใช้</h1>
    <p>กรุณาแก้ไขข้อมูลที่ต้องการ</p>
    <form v-on:submit.prevent="editUser">
      <div class="form-group">
        <input type="text" v-model="user.name" placeholder="ชื่อ" required @focus="showTooltip('กรุณาแก้ไขชื่อ')" @blur="hideTooltip" />
        <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
      </div>
      <div class="form-group">
        <input type="text" v-model="user.lastname" placeholder="นามสกุล" required @focus="showTooltip('กรุณาแก้ไขนามสกุล')" @blur="hideTooltip" />
        <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
      </div>
      <div class="form-group">
        <input type="email" v-model="user.email" placeholder="อีเมล" required @focus="showTooltip('แก้ไขอีเมลที่ถูกต้อง')" @blur="hideTooltip" />
        <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
      </div>
      <div class="form-group">
        <input type="password" v-model="user.password" placeholder="รหัสผ่าน" required @focus="showTooltip('แก้ไขรหัสผ่านที่ปลอดภัย')" @blur="hideTooltip" />
        <span class="tooltip" v-if="tooltipVisible">{{ tooltipText }}</span>
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
      },
      tooltipVisible: false,
      tooltipText: ''
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
.edit-user-container {
  padding: 50px;
  max-width: 500px;
  margin: auto;
  background-color: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
}

.edit-user-container h1 {
  font-size: 28px;
  color: #4a4a4a;
  margin-bottom: 15px;
  text-align: center;
}

.edit-user-container p {
  margin-bottom: 25px;
  color: #7a7a7a;
  text-align: center;
  font-size: 16px;
}

.form-group {
  margin-bottom: 20px;
  position: relative;
}

.form-group input {
  width: 100%;
  padding: 14px 18px;
  border: 1px solid #ccc;
  border-radius: 10px;
  font-size: 16px;
  background-color: #fff;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.form-group input:focus {
  border-color: #a5d6a7;
  outline: none;
  box-shadow: 0 0 10px rgba(165, 214, 167, 0.4);
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

.edit-btn {
  padding: 14px 20px;
  width: 100%;
  border: none;
  border-radius: 10px;
  font-size: 18px;
  color: #fff;
  background-color: #42a5f5;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.edit-btn:hover {
  background-color: #1e88e5;
  transform: scale(1.05);
}

.edit-btn:active {
  background-color: #1565c0;
  transform: scale(1.03);
}
</style>
