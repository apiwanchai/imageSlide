<script setup>
const images = ref([
  {
    src: "https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg",
    alt: "Image 1",
  },
  { src: "https://cdn.vuetifyjs.com/images/carousel/sky.jpg", alt: "Image 2" },
  {
    src: "https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg",
    alt: "Image 3",
  },
]);

const categories = ref(["การ์ตูน", "แอคชั่น", "ความรัก"]);
const selectedCategories = ref([]);

const toggleCategory = (category) => {
  if (selectedCategories.value.includes(category)) {
    selectedCategories.value = selectedCategories.value.filter(
      (c) => c !== category
    );
  } else {
    selectedCategories.value.push(category);
  }
};
const selectedSize = ref("");

const selectSize = (size) => {
  if (selectedSize.value === size) {
    selectedSize.value = ""; 
  } else {
    selectedSize.value = size; 
  }
};

const loadMore = () => {
  images.value.push(
    {
      src: "https://cdn.vuetifyjs.com/images/carousel/sky.jpg",
      alt: "Image 4",
    },
    {
      src: "https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg",
      alt: "Image 5",
    }
  );
};
</script>
<template>
  <div class="container">
    <div class="row">
      <div class="row">
        <div class="col-12">
          <h5>ขนาด</h5>
          <div class="d-flex gap-2">
            <button
              type="button"
              class="btn-custom"
              :class="{ 'btn-selected': selectedSize === 'แนวตั้ง' }"
              @click="selectSize('แนวตั้ง')"
            >
              <i class="bi bi-phone me-2"> </i> แนวตั้ง
            </button>

            <button
              type="button"
              class="btn-custom"
              :class="{ 'btn-selected': selectedSize === 'แนวนอน' }"
              @click="selectSize('แนวนอน')"
            >
              <i class="bi bi-tablet-landscape me-2"> </i> แนวนอน
            </button>

            <button
              type="button"
              class="btn-custom"
              :class="{ 'btn-selected': selectedSize === 'จัตุรัส' }"
              @click="selectSize('จัตุรัส')"
            >
              <i class="bi bi-square me-2"> </i> จัตุรัส
            </button>
          </div>
        </div>
      </div>

      <div class="col-12 mt-3">
        <h5>หมวดหมู่</h5>
        <div class="d-flex gap-2">
          <button
            v-for="(category, index) in categories"
            :key="index"
            type="button"
            :class="{
              'btn-custom btn-selected': selectedCategories.includes(category),
              'btn-custom btn-outline-primary':
                !selectedCategories.includes(category),
            }"
            @click="toggleCategory(category)"
          >
            <span v-if="selectedCategories.includes(category)">
              <i class="bi bi-check-circle-fill me-2"></i>
            </span>
            {{ category }}
          </button>
        </div>
      </div>
    </div>

    <div class="row mt-4">
      <h5>สไตร์ภาพ</h5>
      <div class="image-container">
        <div
          class="image-wrapper"
          v-for="(image, index) in images"
          :key="index"
        >
          <img :src="image.src" class="img-fluid" :alt="image.alt" />
          <div class="image-overlay">
            <span>{{ image.alt }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="row mt-5">
      <div class="col-12 text-center">
        <button class="btn btn-primary" @click="loadMore">โหลดเพิ่ม</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.image-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  max-height: 400px;
  overflow-y: auto;
  padding: 10px;
}

.image-wrapper {
  position: relative;
  border: 2px solid transparent;
  transition: border-color 0.3s;
  border-radius: 10px;
}

.image-wrapper:hover {
  border-color: #0d6efd;
  border-radius: 10px;
}

.image-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(255, 255, 255, 0.9);
  color: #000;
  padding: 5px;
  text-align: center;
  display: block;
  transition: all 0.3s;
  border-radius: 30px;
}

.image-wrapper:hover .image-overlay {
  background-color: rgba(173, 216, 230, 0.9);
  color: #0d6efd;
}

.img-fluid {
  width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

.btn-custom {
  border: 2px solid white;
  border-radius: 10px;
  padding: 10px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 120px;
  text-align: center;
  transition: all 0.3s;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

.btn-btn-custom i {
  margin-right: 5px;
}

.btn-selected {
  background-color: #b3e5fc;
  border: 1px solid #0d6efd;
  color: #0d6efd;
}

.btn-selected i {
  color: #0d6efd;
}
.btn-outline-primary {
  display: flex;
  align-items: center;
  gap: 5px;
}
</style>
