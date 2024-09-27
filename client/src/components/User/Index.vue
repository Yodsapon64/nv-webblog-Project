<template>
  <div class="index-container">
    <h1>รายชื่อผู้ใช้ทั้งหมด</h1>
    <div class="header-actions">
      <button v-on:click="navigateTo('/user/create')" class="create-btn">สร้างผู้ใช้</button>
    </div>
    <hr>
    <div v-if="users.length" class="user-list">
      <div><b>จำนวนผู้ใช้งาน:</b> {{ users.length }}</div>
      <div v-for="user in users" v-bind:key="user.id" class="user-card">
        <div><b>id:</b> {{ user.id }}</div>
        <div><b>ชื่อผู้ใช้:</b> {{ user.name }} {{ user.lastname }}</div>
        <div><b>อีเมล:</b> {{ user.email }}</div>
        <div><b>สถานะ:</b> {{ user.status }}</div>
        <div><b>ประเภท:</b> {{ user.type }}</div>
        <div class="user-actions">
          <button v-on:click="navigateTo('/user/'+user.id)" class="view-btn">ดูข้อมูล</button>
          <button v-on:click="navigateTo('/user/edit/'+user.id)" class="edit-btn">แก้ไขข้อมูล</button>
          <button v-on:click="deleteUser(user)" class="delete-btn">ลบข้อมูล</button>
        </div>
        <hr>
      </div>
    </div>
    <div class="footer-actions">
      <button v-on:click="logout" class="logout-btn">ออกจากระบบ</button>
    </div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";
export default {
  data(){
    return {
      users: []
    }
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('setToken', null);
      this.$store.dispatch('setUser', null);
      this.$router.push({ name: 'login' });
    },
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user) {
      let result = confirm("คุณต้องการลบข้อมูลใช่หรือไม่?");
      if (result) {
        try {
          await UsersService.delete(user);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      try {
        this.users = (await UsersService.index()).data;
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style scoped>
.index-container {
  padding: 40px;
  max-width: 800px;
  margin: auto;
}

h1 {
  text-align: center;
  font-size: 24px;
  color: #333;
}

.header-actions, .footer-actions {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.create-btn, .logout-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  text-transform: uppercase;
  color: #fff;
  background-color: #ff790b;
}

.create-btn:hover, .logout-btn:hover {
  background-color: #e66b00;
  transform: scale(1.05);
}

.create-btn:active, .logout-btn:active {
  background-color: #cc5e00;
  transform: scale(1.03);
}

.user-list {
  margin-top: 20px;
}

.user-card {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
}

.user-actions {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

.view-btn, .edit-btn, .delete-btn {
  padding: 8px 15px;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  color: #fff;
}

.view-btn {
  background-color: #007bff;
}

.view-btn:hover {
  background-color: #0056b3;
}

.edit-btn {
  background-color: #28a745;
}

.edit-btn:hover {
  background-color: #218838;
}

.delete-btn {
  background-color: #dc3545;
}

.delete-btn:hover {
  background-color: #c82333;
}

button:active {
  transform: scale(1.03);
}
</style>
