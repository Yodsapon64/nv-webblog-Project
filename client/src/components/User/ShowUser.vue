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
      <p><strong>สร้างเมื่อ:</strong> {{ formattedDate(user.createdAt) }}</p>
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
      const userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    formattedDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' };
      return new Date(date).toLocaleDateString('th-TH', options);
    }
  }
};
</script>

<style scoped>
.show-user-container {
  padding: 40px;
  max-width: 600px;
  margin: auto;
  background-color: #f4f6f9;
  border-radius: 10px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
  font-size: 26px;
  margin-bottom: 30px;
}

.user-details {
  line-height: 1.8;
  color: #555;
  font-size: 17px;
}

.user-details p {
  margin-bottom: 15px;
}

.user-details p strong {
  color: #333;
}

@media (max-width: 768px) {
  .show-user-container {
    padding: 20px;
  }

  h1 {
    font-size: 22px;
  }

  .user-details {
    font-size: 15px;
  }
}
</style>
