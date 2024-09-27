<template>
  <div class="show-user-container">
    <h1>รายละเอียดผู้ใช้</h1>
    <div class="user-details">
      <p><strong>ID:</strong> {{ user.id }}</p>
      <p><strong>ชื่อ:</strong> {{ user.name }}</p>
      <p><strong>นามสกุล:</strong> {{ user.lastname }}</p>
      <p><strong>อีเมล:</strong> {{ user.email }}</p>
      <p><strong>สถานะ:</strong> {{ user.status }}</p>
      <p><strong>ประเภท:</strong> {{ user.type }}</p>
      <p><strong>สร้างเมื่อ:</strong> {{ user.createdAt }}</p>
    </div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      user: {}
    };
  },
  async created() {
    try {
      var userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style scoped>
.show-user-container {
  padding: 40px;
  max-width: 600px;
  margin: auto;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
  font-size: 24px;
  margin-bottom: 30px;
}

.user-details {
  line-height: 1.6;
  color: #444;
  font-size: 16px;
}

.user-details p {
  margin-bottom: 10px;
}

.user-details p strong {
  color: #555;
}

</style>
