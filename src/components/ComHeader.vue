<template>
  <header>
    <div class="container">
      <div class="logo">
        <img :src="logo" alt="Jaystoree Logo" />
      </div>
      <nav>
        <ul>
          <li><router-link to="/"></router-link></li>
          <li><router-link to="/newarrivals">New Arrivals</router-link></li>
          <li><router-link to="/tops">Tops</router-link></li>
          <li><router-link to="/bottoms">Bottoms</router-link></li>
          <li><router-link to="/outerwear">Outerwear</router-link></li>
          <li><router-link to="/saleoff">Sale Off</router-link></li>
        </ul>
      </nav>

      <!--phần đăng nhập, đăng kí & hiển thị user
      <div class="account">
        <template v-if="user">
          <p>Xin chào, {{ user.username }}</p>
          <button @click="logout">Đăng Xuất</button>
        </template>
        <template v-else>
          <router-link to="/register">Đăng ký</router-link>
          <router-link to="/login">Đăng nhập</router-link>
        </template>
      </div>-->

      <div class="account">
        <template v-if="user">
          <router-link to="/admin" class="username">
            Xin chào, {{ user.username }}
          </router-link>
          <button @click="logout">Đăng Xuất</button>
        </template>
        <template v-else>
          <router-link to="/register">Đăng ký</router-link>
          <router-link to="/login">Đăng nhập</router-link>
        </template>
      </div>

      <!--hiển thị giỏ hàng-->
      <div class="cta">
        <img :src="icon" alt="icon shoppingCart" />
        <router-link to="/cart">Giỏ hàng</router-link>
      </div>
    </div>
  </header>
  <!-- lấy nội dung component được link tới thì dùng -->
  <router-view />
</template>

<script>
import logo from "@/assets/logo_jay.png";
import icon from "@/assets/icon/shopping-cart.png";
import eventBus from "@/eventBus";
export default {
  data() {
    return {
      user: JSON.parse(localStorage.getItem("currentUser")) || null,
      logo,
      icon,
    };
  },

  // nhận tín hiệu từ ComLogin để hiển thị user trong header
  created() {
    eventBus.on("loginSuccess", (user) => {
      this.user = user;
    });
  },

  beforeUnmount() {
    eventBus.off("loginSuccess"); // gỡ bỏ lắng nghe
  },

  methods: {
    logout() {
      localStorage.removeItem("currentUser");
      this.user = null;
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
header {
  background-color: #000; /* Nền đen */
  color: #fff; /* Chữ trắng */
  padding: 15px 40px; /* Khoảng cách bên trong */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Hiệu ứng bóng cho header */
  position: sticky; /* Header luôn ở trên cùng */
  top: 0;
  z-index: 1000;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.logo img {
  height: 70px; /* Chiều cao logo */
}

nav ul {
  list-style: none;
  display: flex;
  gap: 50px; /* Khoảng cách giữa các mục */
  padding: 0;
  margin: 0;
}

nav ul li {
  font-size: 16px;
  text-transform: uppercase; /* Chữ in hoa */
}

nav ul li a {
  text-decoration: none;
  color: #fff; /* Màu chữ trắng */
  transition: color 0.3s ease, transform 0.3s ease;
}

nav ul li a:hover {
  color: #ccc; /* Đổi sang màu xám nhạt khi hover */
  transform: scale(1.1); /* Phóng to nhẹ khi hover */
}

.account {
  display: flex;
  align-items: center;
  gap: 15px;
}

.account p {
  margin: 0;
  font-size: 14px;
  color: #ccc;
}

.account button {
  background-color: transparent;
  border: 1px solid #fff;
  color: #fff;
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.account button:hover {
  background-color: #fff;
  color: #000;
}

.account a {
  text-decoration: none;
  color: #fff;
  font-size: 14px;
  border: 1px solid #fff;
  padding: 5px 10px;
  border-radius: 4px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.account a:hover {
  background-color: #fff;
  color: #000;
}
.cta {
  display: flex;
  align-items: center;
  gap: 10px;
}

.cta img {
  height: 24px; /* Kích thước icon */
  width: 24px;
}

.cta a {
  text-decoration: none;
  color: #fff;
  font-size: 14px;
  transition: color 0.3s ease;
}

.cta a:hover {
  color: #ccc; /* Đổi sang màu xám nhạt khi hover */
}

@media (max-width: 768px) {
  nav ul {
    flex-direction: column; /* Xếp dọc trên màn hình nhỏ */
    gap: 10px;
  }

  .container {
    flex-wrap: wrap; /* Tự động xuống dòng khi không đủ chỗ */
  }

  .cta {
    margin-top: 10px;
  }
}
</style>