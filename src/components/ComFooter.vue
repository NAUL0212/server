<template>
   <footer>
        <div class="footer-container">
            <div class="footer-column">
                <h5>HỆ THỐNG CỬA HÀNG JAYSTOREE</h5>
                <p>Store 1: 648 Sư Vạn Hạnh, Quận 10</p>
                <p>Store 2: 352 Huỳnh Văn Bánh, Quận Phú Nhuận</p>
            </div>
            <div class="footer-column">
                <h5>CHÍNH SÁCH</h5>
                <ul>
                    <li><a href="#">Chính sách sử dụng website</a></li>
                    <li><a href="#">Hướng dẫn mua hàng</a></li>
                    <li><a href="#">Phương thức thanh toán</a></li>
                    <li><a href="#">Chính sách giao nhận - vận chuyển</a></li>
                    <li><a href="#">Chính sách đổi và bảo hành sản phẩm</a></li>
                </ul>
            </div>
            <div class="footer-column">
                <h5>THÔNG TIN LIÊN HỆ</h5>
                <p>CÔNG TY TNHH JASYTOREE</p>
                <p>SỐ CSKH: 0935297000 (10h -18h)</p>
                <p>Website: jaystoree.vn</p>
                <p>jaystoree@gmail.column</p>
            </div>

            <div class="footer-column">
                <h5>FOLLOW US ON SOCIAL MEDIA</h5>
                <ul>
                    <li><a href="https://www.facebook.com/jay.storee?locale=vi_VN" target="_blank" rel="noopener noreferrer">Facebook</a></li>
                    <li><a href="https://www.instagram.com/jay.storee/" target="_blank" rel="noopener noreferrer">Instagram</a></li>
                </ul>
            </div>
        </div>
    </footer>
</template>

<script>
export default {

}
</script>

<style scoped>


.footer-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: flex-start;
    background-color: #000; /* Nền đen */
    color: #fff; /* Chữ trắng */
    padding: 30px 40px; /* Khoảng cách bên trong */
    gap: 20px;
    border-top: 2px solid #fff; /* Đường kẻ trắng trên cùng */
}

.footer-column {
    flex: 1 1 calc(25% - 20px); /* Mỗi cột chiếm 1/4 chiều rộng */
    min-width: 200px;
    text-align: left;
}

.footer-column h4 {
    font-size: 18px;
    margin-bottom: 15px;
    color: #fff; /* Chữ trắng nổi bật */
    text-transform: uppercase; /* Chữ in hoa */
    border-bottom: 1px solid #fff; /* Đường kẻ trắng dưới tiêu đề */
    padding-bottom: 5px;
}

.footer-column p,
.footer-column ul li {
    font-size: 14px;
    margin-bottom: 10px;
    line-height: 1.6;
    color: #ccc; /* Chữ xám nhạt để dễ đọc */
}

.footer-column ul {
    list-style-type: none;
    padding: 0;
}

.footer-column ul li a {
    text-decoration: none;
    color: #fff; /* Chữ trắng cho liên kết */
    transition: color 0.3s ease;
}

.footer-column ul li a:hover {
    color: #ccc; /* Đổi sang màu xám nhạt khi hover */
}

.footer-column:last-child ul {
    display: flex; /* Xếp liên kết mạng xã hội ngang hàng */
    gap: 10px;
}

.footer-column:last-child ul li a {
    color: #fff; /* Chữ trắng mặc định */
    font-size: 16px;
    transition: color 0.3s ease, transform 0.3s ease;
}

.footer-column:last-child ul li a:hover {
    color: #ccc; /* Chữ xám nhạt khi hover */
    transform: scale(1.1); /* Hiệu ứng phóng to nhẹ khi hover */
}

.footer-container p {
    color: #ccc; /* Chữ xám nhạt */
    text-align: left; /* Căn lề trái */
}

@media (max-width: 768px) {
    .footer-container {
        flex-direction: column; /* Xếp các cột dọc trên màn hình nhỏ */
        gap: 30px;
    }
}
</style>