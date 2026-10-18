<template>
  <!-- Container หลัก -->
  <div class="container my-5">

    <!-- หัวข้อ -->
    <h2 class="text-center mb-3">แสดงข้อมูลสินค้า</h2>

    <!-- ปุ่มดึงข้อมูล -->
    <div class="text-center mb-4">
      <button 
        type="button" 
        class="btn btn-primary"
        @click="fetchProducts"
      >
        อัปเดต
      </button>
    </div>

    <!-- ตารางสินค้า -->
    <div class="table-responsive">
      <table class="table table-bordered table-striped align-middle">

        <!-- ส่วนหัวตาราง -->
        <thead class="table-dark text-center">
          <tr>
            <th width="100">รหัสสินค้า</th>
            <th width="120">รูปภาพ</th>
            <th>ชื่อสินค้า</th>
            <th width="120">จำนวน</th>
            <th width="120">ราคา</th>
          </tr>
        </thead>

        <!-- ส่วนข้อมูลสินค้า -->
        <tbody>

          <!-- วนลูปแสดงสินค้า -->
          <tr v-for="product in products" :key="product.id">
            <!-- รหัสสินค้า -->
            <td class="text-center">
              {{ product.id }}
            </td>

            <!-- รูปภาพ -->
            <td class="text-center">
              <img
                :src="product.thumbnail"
                alt="Product Image"
                width="80"
                height="60"
                style="object-fit: contain"
              />
            </td>

            <!-- ชื่อสินค้า -->
            <td>
              <a href="#" class="text-decoration-none">{{ product.title }}</a>
            </td>

            <!-- จำนวน (Stock) -->
            <td class="text-center">
              {{ product.stock }}
            </td>

            <!-- ราคา (สีแดง) -->
            <td class="text-center text-danger fw-bold">
              ${{ product.price }}
            </td>
          </tr>

        </tbody>
      </table>
    </div>

  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    // สร้างตัวแปร products เพื่อเก็บข้อมูลสินค้า
    const products = ref([]);

    // ฟังก์ชันดึงข้อมูลสินค้าจาก API
    const fetchProducts = async () => {
      try {
        const response = await fetch("https://dummyjson.com/products");
        const data = await response.json();
        products.value = data.products;
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    };

    return {
      products,
      fetchProducts, // ส่งออกฟังก์ชันเพื่อให้กดปุ่ม "ดึงข้อมูล" ได้
    };
  },
};
</script>