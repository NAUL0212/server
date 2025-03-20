<template>
  <div class="register-form">
    <h2>Đăng ký tài khoản</h2>
    <input  v-model="username" placeholder="Tên đăng nhập" />
    <input  v-model="password" type="password" placeholder="Mật khẩu" />
    <input v-model="confirmPassword" type="password" placeholder="Xác nhận mật khẩu" />
    <button @click="register">Đăng ký</button>
    <p v-if="error"  class="error">{{error}}</p>
    <p v-if="success" class="success">{{success}}</p>
  </div>
</template>

<script>
import users from '@/data/users'

export default {
  data() {
    return {
      username: "",
      password: "",
      confirmPassword: "",
      error: "",
      success: "",
    users:users
    };
  },
  methods:{
    register(){
        // kiểm tra password và confirm password phải giống nhau
        if(this.password !== this.confirmPassword){
            this.error="Mật khẩu đăng ký không khớp"
            return
        }

        //kiểm tra user này có tồn tại dưới localStorage hay không
        const users = JSON.parse(localStorage.getItem('users')) || [];

        // kiểm tra username có tồn tại trong database hay chưa
        const exituser = this.users.find(x => x.username === this.username)
        if(exituser)
        {
            this.error="Tên đã tồn tại"
            return
        }

        // nếu ko tồn tại thì add vào data user
        // 1. tạo đối tượng
        const newUser = {id: this.users.length+1, username: this.username, password: this.password, confirmPassword: this.confirmPassword}
        // 2. đẩy newUser vào danh sách (users)
        this.users.push(newUser)
        // 3. lưu danh sách xuống local Storage
        localStorage.setItem('users', JSON.stringify(users))
        this.success="Đăng ký thành công"
        this.error=''
        this.username=''
        this.password=''
        this.confirmPassword=''
        // cách điều hướng nhanh: this.$router.push(path)
        this.$router.push('/login')
    }
  }
  
};
</script>

<style scoped>
/* Căn giữa form đăng ký */
.register-form {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f7f7f7;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  text-align: center;
}

.register-form h2 {
  color: #333;
  margin-bottom: 20px;
}

/* Định dạng input */
.register-form input[type="text"],
.register-form input[type="password"] {
  width: calc(100% - 22px); /* Giảm chiều rộng để trừ khoảng padding */
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
}

/* Định dạng nút */
.register-form button {
  width: 100%;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.register-form button:hover {
  background-color: #45a049;
}

/* Định dạng thông báo lỗi */
.error {
  color: #d9534f;
  font-size: 14px;
  margin-top: 10px;
}

/* Định dạng thông báo thành công */
.success {
  color: #5cb85c;
  font-size: 14px;
  margin-top: 10px;
}
</style>