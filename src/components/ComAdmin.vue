<template>
  <div class="admin">
    <h1>Quản lý sản phẩm</h1>

    <!-- Form thêm sản phẩm -->
    <h2>Thêm sản phẩm mới</h2>
    <form @submit.prevent="handleAddProduct">
      <div class="form-group">
        <label for="name">Tên sản phẩm:</label>
        <input id="name" v-model="newProduct.name" required placeholder="Tên sản phẩm" />
      </div>

      <div class="form-group">
        <label for="image">Hình ảnh:</label>
        <input id="image" v-model="newProduct.image" required placeholder="Đường dẫn ảnh" />
      </div>

      <div class="form-group">
        <label for="price">Giá:</label>
        <input id="price" v-model.number="newProduct.price" type="number" required placeholder="Giá sản phẩm" />
      </div>

      <div class="form-group">
        <label for="category">Danh mục:</label>
        <input id="category" v-model="newProduct.category" required placeholder="Danh mục sản phẩm" />
      </div>

      <div class="form-group">
        <label for="size">Kích cỡ:</label>
        <input id="size" v-model="sizeInput" placeholder="Nhập các kích cỡ, cách nhau bởi dấu phẩy" />
      </div>

      <div class="form-group">
        <label for="description">Mô tả:</label>
        <textarea id="description" v-model="newProduct.description" placeholder="Mô tả sản phẩm"></textarea>
      </div>

      <div class="form-group">
        <label for="stock">Số lượng tồn kho:</label>
        <input id="stock" v-model.number="newProduct.stock" type="number" required placeholder="Số lượng tồn kho" />
      </div>

      <button type="submit">Thêm sản phẩm</button>
    </form>

    <!-- Danh sách sản phẩm -->
    <h2>Danh sách sản phẩm</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Tên sản phẩm</th>
          <th>Danh mục</th>
          <th>Giá</th>
          <th>Tồn kho</th>
          <th>Thao tác</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.category }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.stock }}</td>
          <td>
            <button @click="deleteProduct(product.id)">Xóa</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      products: [], // Danh sách sản phẩm
      newProduct: {
        name: "",
        image: "",
        price: 0,
        category: "",
        size: [],
        description: "",
        stock: 0,
      },
      sizeInput: "", // Chuỗi nhập từ người dùng cho kích cỡ
    };
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get("http://localhost:3000/api/products");
        this.products = response.data;
      } catch (error) {
        console.error("Lỗi khi tải danh sách sản phẩm:", error);
      }
    },

    async handleAddProduct() {
      try {
        // Chuyển sizeInput từ chuỗi thành mảng M, L, XL => [M, L, XL]
        this.newProduct.size = this.sizeInput.split(",").map((size) => size.trim());

        // Gửi yêu cầu POST để thêm sản phẩm
        const response = await axios.post("http://localhost:3000/api/products", this.newProduct);

        // Thêm sản phẩm mới vào danh sách hiển thị
        this.products.push(response.data);

        // Reset form
        this.newProduct = {
          name: "",
          image: "",
          price: 0,
          category: "",
          size: [],
          description: "",
          stock: 0,
        };
        this.sizeInput = "";

        alert("Thêm sản phẩm thành công!");
      } catch (error) {
        console.error("Lỗi khi thêm sản phẩm:", error);
      }
    },

    async deleteProduct(id) {
      try {
        await axios.delete(`http://localhost:3000/api/products/${id}`);
        this.products = this.products.filter((product) => product.id !== id);
        alert("Xóa sản phẩm thành công!");
      } catch (error) {
        console.error("Lỗi khi xóa sản phẩm:", error);
      }
    },
  },
  mounted() {
    this.fetchProducts(); // Tải danh sách sản phẩm khi component được mount
  },
};
</script>

<style scoped>
.admin {
  padding: 20px;
}
h1, h2 {
  margin-bottom: 20px;
}
form {
  margin-bottom: 40px;
}
form .form-group {
  margin-bottom: 10px;
}
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
table, th, td {
  border: 1px solid #ddd;
}
th, td {
  padding: 8px;
  text-align: left;
}
button {
  padding: 5px 10px;
  margin-right: 5px;
  cursor: pointer;
}
</style>