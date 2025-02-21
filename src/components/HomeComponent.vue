<template>
	<div class="image-container">
		<div class="image-wrapper">
			<img :src="imageSrc" alt="" class="fade-img" />
		</div>
		<div class="overlay"></div>
		<div class="home-title">
			<h3>Welcome to Yalova</h3>
			<div class="title">
				<div></div>
				<p>Responsive restaurant template</p>
				<div></div>
			</div>
			<div class="half-circle">
				<i style="margin-top: 10px" class="fa-solid fa-star"></i>
			</div>
		</div>
		<div class="angles">
			<button class="angles-left-btn" @click="changeImage">
				<i class="fa-solid fa-angle-left fa-2xl"></i>
			</button>
			<div class="dots">
				<span
					v-for="(dot, index) in images"
					:key="index"
					:class="['dot', { active: currentIndex === index }]"
				></span>
			</div>
			<button class="angles-right-btn" @click="changeImage">
				<i class="fa-solid fa-angle-right fa-2xl"></i>
			</button>
		</div>
	</div>
	<DiscoverComponent />
	<OpenHourComponent />
	<OurRestaurantComponent />
	<WeeklyDealsComponent />
	<OurTeamComponent />
</template>


<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import {
	DiscoverComponent,
	OpenHourComponent,
	OurRestaurantComponent,
	WeeklyDealsComponent,
	OurTeamComponent,
} from './homeComponent/index';

const images = [
	'../src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
	'../src/assets/shef.jpg',
];

const imageSrc = ref(images[0]);
let currentIndex = 0;
let interval = null;

const changeImage = (isManual = false) => {
	if (isManual) {
		document.querySelector('.fade-img').classList.add('fade-out');
		currentIndex = (currentIndex + 1) % images.length;
		imageSrc.value = images[currentIndex];
		document.querySelector('.fade-img').classList.remove('fade-out');
	} else {
		document.querySelector('.fade-img').classList.add('fade-out');
		setTimeout(() => {
			currentIndex = (currentIndex + 1) % images.length;
			imageSrc.value = images[currentIndex];
			document.querySelector('.fade-img').classList.remove('fade-out');
		}, 3000); 
	}
};

onMounted(() => {
	interval = setInterval(() => {
		changeImage(false); 
	}, 8000); 
});

onUnmounted(() => {
	clearInterval(interval);
});
</script>



<style lang="scss" scoped>
.image-container {
	position: relative;
	width: 100%;
	height: 100vh;

	.image-wrapper {
		width: 100%;
		height: 100%;
		overflow: hidden;
		position: fixed;
		top: 0;
		left: 0;
		z-index: 0;
	}

	.fade-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: opacity 1s ease-in-out; 
	}

	.fade-img.fade-out {
		opacity: 0.5;
	}

	.overlay {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: var(--black);
		z-index: 1;
		opacity: 0.5;
	}

	.angles {
		display: flex;
		align-items: center;
		position: absolute;
		top: 80%;
		width: 100%;
		justify-content: center;
		gap: 20px;

		.angles-left-btn {
			background-color: transparent;
			border: none;
			color: var(--white);
			position: relative;
			z-index: 2;
			cursor: pointer;
		}

		.dots {
			display: flex;
			gap: 8px;
			justify-content: center;
			align-items: center;

			.dot {
				width: 10px;
				height: 10px;
				background-color: var(--light-gray); 
				border-radius: 50%;
				opacity: 0.7;
				transition: background-color 0.3s ease;
			}

			.dot.active {
				background-color: var(--primary);
			}
		}

		.angles-right-btn {
			background-color: transparent;
			border: none;
			color: var(--white);
			position: relative;
			z-index: 2;
			cursor: pointer;
		}
	}

	.home-title {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		color: var(--white);
		z-index: 2;
		text-align: center;

		h3 {
			width: 100%;
			font-size: 3.5em;
			margin-bottom: 10px;
			color: var(--white);
			font-weight: bold;
			letter-spacing: 3px;
			font-family: 'Playball', cursive;
		}

		.title {
			display: flex;
			place-items: center;
			div {
				width: 80px;
				height: 0.5px;
				background: var(--primary);
			}
		}

		p {
			font-size: 14px;
			text-transform: uppercase;
			letter-spacing: 2px;
			color: var(--white);
			max-width: 350px;
			margin: 0 auto;
		}

		.half-circle {
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			margin-top: 130px;
			width: 100px;
			height: 50px;
			border-bottom-left-radius: 200px;
			border-bottom-right-radius: 200px;
			border: 5px solid var(--primary);
			border-top: 0 !important;
		}
	}

	@media screen and (max-width: 1030px) {
		.home-title {
			h3 {
				font-size: 22px;
			}

			p {
				font-size: 12px;
			}

			.title {
				div {
					display: none;
				}
			}
		}
	}
}
</style>

