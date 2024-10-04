<template>
  <div class="login-user-container">
    <div class="login-card">
      <div class="login-left">
        <img src="@/assets/dragon ball.jpg" alt="Login Image"> <!-- เส้นทางรูปภาพ -->
      </div>
      <div class="login-right">
        <h1>เข้าสู่ระบบ</h1>
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
  padding: 20px;
}

.login-card {
  background-color: #d8d8d8;
  box-shadow: 0 4px 8px rgba(255, 116, 3, 0.1);
  border-radius: 10px;
  overflow: hidden;
  display: flex;
  max-width: 800px;
  width: 100%;
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
  padding: 40px;
  flex: 1;
}

.login-right h1 {
  margin-bottom: 20px;
  font-size: 24px;
  color: #333;
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
  position: relative;
}

.form-group label {
  margin-bottom: 5px;
  font-weight: bold;
  color: #555;
}

.form-group input {
  padding: 12px 15px;
  width: 100%;
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

.login-btn {
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

.login-btn:hover {
  background-color: #e66b00;
  transform: scale(1.05);
}

.error {
  margin-top: 10px;
  color: red;
}
</style>
