<template>
  <div class="login-user-container">
    <div class="login-card">
      <div class="login-left">
        <img src="@/assets/evangelion.jpg" alt="Login Image"> <!-- เส้นทางรูปภาพ -->
      </div>
      <div class="login-right">
        <h1>เข้าสู่ระบบ</h1>
        <p class="login-description">กรุณากรอกอีเมลและรหัสผ่านเพื่อเข้าสู่ระบบ</p>
        <form v-on:submit.prevent="onLogin" class="login-form">
          <div class="form-group">
            <label for="email">อีเมล</label>
            <input type="email" id="email" name="email" v-model="email" required />
          </div>
          <div class="form-group">
            <label for="password">รหัสผ่าน</label>
            <input type="password" id="password" name="password" v-model="password" required />
          </div>
          <button type="submit" class="login-btn">เข้าสู่ระบบ</button>
          <div class="error" v-if="error">{{ error }}</div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import AuthenService from "../services/AuthenService";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: null,
    };
  },
  methods: {
    async onLogin() {
      try {
        const response = await AuthenService.login({
          email: this.email,
          password: this.password,
        });

        this.$store.dispatch("setToken", response.data.token);
        this.$store.dispatch("setUser", response.data.user);

        this.$router.push({
          name: "users",
        });
      } catch (error) {
        console.log(error);
        this.error = error.response.data.error;
        this.email = "";
        this.password = "";
      }
    },
  },
};
</script>

<style scoped>
.login-user-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f5f5f5;
}

.login-card {
  background-color: #ffffff;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  max-width: 900px;
  width: 100%;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.login-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.15);
}

.login-left {
  flex: 1;
  position: relative;
}

.login-left img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.login-right {
  padding: 50px;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1 {
  font-size: 28px;
  color: #333;
  margin-bottom: 10px;
}

.login-description {
  font-size: 16px;
  color: #666;
  margin-bottom: 30px;
}

.login-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  font-size: 14px;
  color: #333;
  margin-bottom: 5px;
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
  box-shadow: 0 0 10px rgba(255, 120, 11, 0.3);
  outline: none;
}

.login-btn {
  padding: 15px;
  border: none;
  border-radius: 8px;
  font-size: 18px;
  cursor: pointer;
  margin-top: 20px;
  background-color: #ff790b;
  color: #fff;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.login-btn:hover {
  background-color: #e66b00;
  transform: scale(1.05);
}

.error {
  margin-top: 20px;
  color: red;
  font-size: 14px;
}

@media (max-width: 768px) {
  .login-card {
    flex-direction: column;
  }

  .login-left {
    height: 200px;
  }

  .login-right {
    padding: 30px;
  }
}
</style>
