<template>
    <div class="listprod">
        <h2 class="prodhead">รายการสินค้าทั้งหมด</h2>
        <div class="dropdown-container" ref="dropdownRef">
            <!-- ปุ่มกดเลือกประเภทสินค้า -->
            <span @click="toggleDropdown" class="dropdown-btn">
                {{ selectedCategory || "เลือกประเภทสินค้า" }} 
            </span>

            <!-- Dropdown เมนู -->
            <transition name="dropdown">
            <ul v-if="isOpen" class="dropdown-menu">
                <li v-for="category in categories" :key="category" @click="selectCategory(category)">
                    {{ category }}
                </li>
            </ul>
            </transition>
        </div>
        <div class="product">

        </div>
        <div class="product" style="margin-left: -590px;">

        </div>
        <div class="product" style="margin-left: -340px;">

        </div>
        <div class="product" style="margin-left: -90px;">

        </div>
        <div class="product" style="margin-top: 180px;">

        </div>
        <div class="product" style="margin-left: -590px; margin-top: 180px;">

        </div>
        <div class="product" style="margin-left: -340px; margin-top: 180px;">

        </div>
        <div class="product" style="margin-left: -90px; margin-top: 180px;">

        </div>
        <button class="backtosearch">กลับหน้าค้นหาสินค้า</button>
    </div>
</template>

<style scoped>

.listprod{
  background-color: #ccfe58;
  box-shadow: 0 8px 8px rgba(0, 0, 0, 0.2);
  border: 3px solid black;
  border-radius: 30px;
  display: flexbox;
  padding-left: 1250px;
  padding-bottom: 180px;
  color: black;
  position: fixed;
  margin-top: 110px;
  margin-bottom: 10px;
  margin-left: 60px;
  margin-right: 40px;
  height: 400px;
  width: 150px;
}

.prodhead{
  margin-left: -1200px;
  margin-top: 10px;
}

.product{
  background-color: #fbfe58;
  box-shadow: 0 8px 8px rgba(0, 0, 0, 0.2);
  border: 3px solid black;
  border-radius: 30px;
  display: flexbox;
  padding-left: 170px;
  padding-bottom: 170px;
  color: black;
  position: fixed;
  margin-top: -50px;
  margin-bottom: 10px;
  margin-left: -840px;
  height: 10px;
  width: 10px;
}

.dropdown-container {
  margin-left: -1000px;
  width: 250px;
}

.dropdown-btn {
  display: block;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  background-color: white;
  cursor: pointer;
  text-align: center;
  border-radius: 5px;
  margin-left: -200px;
  background-color: rgb(255, 120, 255);
}

.dropdown-menu {
  position: absolute;
  width: 18.5%;
  background: white;
  border: 1px solid #ddd;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  margin-top: 5px;
  list-style: none;
  margin-left: -320px;
  padding: 0;
}

.dropdown-menu li {
  padding: 10px;
  cursor: pointer;
}

.dropdown-menu li:hover {
  background-color: #f0f0f0;
}

/* CSS Animation */
.dropdown-enter-active, .dropdown-leave-active {
  transition: all 0.3s ease;
}

.dropdown-enter-from, .dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

button.backtosearch {
  width: 100%;
  padding: 20px;
  background-color: #006eb3;
  color: rgb(85, 255, 43);
  border:2px solid blue;
  border-radius: 4px;
  cursor: pointer;
  font-size: 20px;
  -webkit-text-stroke: 0.5px rgb(0, 228, 0);
  margin-left: -2270px;
  margin-top: 300px;
}

button.backtosearch:hover {
  background-color: #64f0ff;
}

</style>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isOpen = ref(false);
const selectedCategory = ref(null);
const dropdownRef = ref(null);

// รายการประเภทสินค้า
const categories = ref(["All", "อาหาร", "อุปกรณ์อิเล็กทรอนิกส์", "ของใช้ทั่วไป"]);

// เปิด/ปิด Dropdown
const toggleDropdown = () => {
  isOpen.value = !isOpen.value;
};

// เลือกประเภทสินค้า
const selectCategory = (category) => {
  selectedCategory.value = category;
  isOpen.value = false; // ปิด dropdown หลังจากเลือก
};

// ปิด dropdown ถ้าคลิกข้างนอก
const handleClickOutside = (event) => {
  if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    isOpen.value = false;
  }
};

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onUnmounted(() => {
  document.removeEventListener("click", handleClickOutside);
});
</script>
