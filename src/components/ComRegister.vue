<template>
  <div class="register-form">
    <h2>Đăng ký tài khoản</h2>
    <input v-model="username" placeholder="Tên đăng nhập" />
    <input v-model="password" type="password" placeholder="Mật khẩu" />
    <input v-model="confirmPassword" type="password" placeholder="Xác nhận mật khẩu" />
    <button @click="register">Đăng ký</button>
    <p v-if="error" class="error">{{ error }}</p>
    <p v-if="success" class="success">{{ success }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      password: '',
      confirmPassword: '',
      error: '',
      success: ''
    };
  },
  methods: {
    async register() {
      this.error = '';
      this.success = '';

      if (this.password !== this.confirmPassword) {
        this.error = 'Mật khẩu đăng ký không khớp';
        return;
      }

      try {
        const response = await axios.post('http://localhost:3000/user/register', {
          username: this.username,
          password: this.password
        });

        this.success = response.data.message || 'Đăng ký thành công';
        this.username = '';
        this.password = '';
        this.confirmPassword = '';

        // Chuyển hướng đến trang đăng nhập
        setTimeout(() => {
          this.$router.push('/login');
        }, 1500);
      } catch (error) {
        this.error = error.response?.data?.message || 'Đăng ký thất bại';
      }
    }
  }
};
</script>

<style scoped>
/* CSS giữ nguyên */
</style>
