<template>
  <div>
    <h2>Đăng nhập</h2>
    <input v-model="username" placeholder="Tên đăng nhập" />
    <input v-model="password"  type="password" placeholder="Mật khẩu" />
    <button @click="login">Đăng nhập</button>
    <p v-if="error">{{error}}</p>
  </div>
</template>

<script>
import users from '@/data/users'
import eventBus from '@/eventBus'
export default {
  data() {
    return {
      username: '',
      password: '',
      error: '',
      users:users
      
    };
  },
  methods:{
    login(){
        // tìm user khớp với (kiểm tra: username và password đăng nhập === username và password đã register lưu trong database)
        const user = this.users.find(u=> u.username === this.username && u.password === this.password);
        if(user){
            //lưu người dùng vào localStorage nếu đăng nhập thành công
            localStorage.setItem('currentUser', JSON.stringify(user));
            eventBus.emit('loginSuccess', user)          // phát tín hiệu đến ComHeader (cha)
            this.$router.push('/');
        }else{ // không khớp tài khoản, mật khẩu nào hết
            this.error="Tên đăng nhập hoặc mật khẩu không đúng"
        }
    },
    
  }
  
};
</script>
<style scoped>
/* Căn giữa form đăng nhập */
div {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f7f7f7;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  text-align: center;
}

h2 {
  color: #333;
  margin-bottom: 20px;
}

/* Định dạng input */
input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
}

/* Định dạng nút */
button {
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

button:hover {
  background-color: #45a049;
}

/* Định dạng thông báo lỗi */
p {
  color: #d9534f;
  font-size: 14px;
  margin-top: 10px;
}
</style>

