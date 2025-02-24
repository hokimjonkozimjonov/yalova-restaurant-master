<template>
	<div class="pb-10 bg-[var(--black)] opacity-60">
		<ul class="flex justify-between items-center md:mx-20 lg:mx-38">
			<li 
				v-for="item in menuLinks" 
				:key="item.id" 
				data-aos="zoom-in-up" 
				class="p-3 sm:py-4 sm:px-10 rounded-lg bg-[var(--white)] cursor-pointer"
				@click="scrollToSection(item.to)"
			>
				<p class="font-bold sm:text-2xl text-[var(--black)] font-[Playball,cursive] text-center">
					{{ item.name }}
				</p>
				<p class="text-[10px] text-center sm:mt-1 sm:text-lg sm:font-medium text-[var(--primary)]">{{ item.time }}</p>
			</li>
		</ul>
	</div>
</template>

<script setup>
import { menuLinks } from '../menuComponent/index.js';

const scrollToSection = (id) => {
	const section = document.getElementById(id);
	if (section) {
		section.scrollIntoView({ behavior: 'smooth' });
	}
};
</script>
