<template>
  <div class="grid sm:grid-cols-2 md:grid-cols-3 gap-2 md:gap-5 mx-[15%]">
    <div
      v-for="(item, index) in filteredPhotos"
      :key="item.id"
      class="relative flex justify-center"
      :class="{
        'md:col-span-2 row-span-2 max-w-full': index === 3,
        'col-span-1 row-span-2 max-w-full': index === 4,
      }"
    >
      <a @click.prevent="openModal(index)" class="cursor-pointer">
        <img
          data-aos="zoom-in-up"
          :src="item.img"
          class="w-full h-full object-cover rounded-lg transform transition-all duration-200 ease-in-out hover:scale-105"
        />
      </a>
    </div>
  </div>

  <div v-if="isModalOpen" class="relative overflow-hidden">
    <div class="fixed inset-0 w-full h-full flex justify-center items-center">
      <div class="relative rounded-lg md:max-h-[100vh] lg:max-w-[100%] lg:max-h-[80%] bg-white opacity-90 z-10 p-20 group">
        <button class="relative left-[54%] bottom-[50px] text-[var(--black)] cursor-pointer acrive:opacity-50 hover:opacity-50">
          <i @click="closeModal" class="fa-solid fa-xmark fa-2xl"></i>
        </button>

        <div class="flex justify-between items-center gap-5 sm:gap-10 md:gap-30 lg:gap-40">
          <button @click="previousImage" class="text-4xl text-[var(--primary)] cursor-pointer active:opacity-50">
            <i class="fa-solid fa-angle-left fa-lg"></i>
          </button>
          <div class="flex justify-center">
            <img
              :src="filteredPhotos[currentIndex].img"
              class="transition-all duration-500 w-[100%] lg:h-[500px] object-cover rounded-lg"
            />
          </div>
          <button @click="nextImage" class="text-4xl text-[var(--primary)] cursor-pointer active:opacity-50">
            <i class="fa-solid fa-angle-right fa-lg"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, computed } from 'vue';
import { menuPhotos } from '../galleryComponent/index.js'; 

const props = defineProps({
  category: {
    type: String,
    required: true,
  },
});

const isModalOpen = ref(false);
const currentIndex = ref(0);

const filteredPhotos = computed(() => {
  if (props.category === 'All') {
    return menuPhotos; 
  } else {
    return menuPhotos.filter(item => item.categories === props.category.toLowerCase()); 
  }
});

const openModal = (index) => {
  currentIndex.value = index;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const previousImage = () => {
  currentIndex.value = (currentIndex.value - 1 + filteredPhotos.value.length) % filteredPhotos.value.length;
};

const nextImage = () => {
  currentIndex.value = (currentIndex.value + 1) % filteredPhotos.value.length;
};
</script>

<style scoped>
.transition-all {
  transition: all 0.5s ease-in-out;
}
</style>
