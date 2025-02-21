<template>
  <section class="bg-[var(--white)] relative flex items-center justify-center pt-20 pb-30">
    <div class="text-center space-y-6">
      <ul class="flex items-center justify-center gap-3 sm:gap-10">
        <li v-for="item in links" :key="item.id" class="cursor-pointer" data-aos="zoom-in-up">
          <a
            @click.prevent="filterCategory(item.name)"
            :class="{
              'text-[var(--primary)]': selectedCategory === item.name, 
              'text-medium': selectedCategory !== item.name
            }"
            class="font-['Playball',cursive] sm:text-xl"
          >
            {{ item.name }}
          </a>
        </li>
      </ul>

      <div class="my-10 md:my-20 flex items-center justify-center gap-10 md:gap-20">
        <div class="w-20 md:w-40 h-[0.5px] bg-[var(--primary)]"></div>
        <div class="w-2 h-2 rounded-[50%] bg-[var(--black)]"></div>
        <div class="w-20 md:w-40 h-[0.5px] bg-[var(--primary)]"></div>
      </div>

      <GalleryCards :category="selectedCategory" />
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import { links } from '../galleryComponent/index.js'; 
import GalleryCards from '../galleryComponent/GalleryCards.vue';

const selectedCategory = ref('All');

const filterCategory = (category) => {
  selectedCategory.value = category;
};
</script>
