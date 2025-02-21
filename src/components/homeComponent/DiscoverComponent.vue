<template>
	<section class="discover">
		<div class="discover-title">
			<h3 data-aos="zoom-in-up">{{ currentContent.title }}</h3>
			<div class="line" data-aos="zoom-in-up">
				<div>
					<div></div>
					<div></div>
				</div>
				<h5>{{ currentContent.subtitle }}</h5>
				<div>
					<div></div>
					<div></div>
				</div>
			</div>
			<p data-aos="zoom-in-up">
				{{ currentContent.text }}
			</p>

			<RouterLink class="routerLink" to="/menu">
				<h4 data-aos="zoom-in-up">Discover our menu</h4>
			</RouterLink>

			<div class="angles">
				<button class="angles-left-btn" @click="changeContent('left')">
					<i class="fa-solid fa-angle-left fa-2xl"></i>
				</button>
				<div class="dots">
					<span v-for="(dot, index) in contents" :key="index" :class="['dot', { active: currentIndex === index }]"></span>
				</div>
				<button class="angles-right-btn" @click="changeContent('right')">
					<i class="fa-solid fa-angle-right fa-2xl"></i>
				</button>
			</div>
		</div>
		<div class="discover-img" data-aos="zoom-in-up">
			<img :src="currentContent.image" alt="Discover Image" />
		</div>
	</section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const contents = [
	{
		image: '../src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		title: 'Discover',
		subtitle: 'Our Story',
		text: 'Boulanger served salted poultry and fresh eggs, all presented without a tablecloth on small marble tables. He was known for touting for customers outside his establishment, dressed in aristocratic fashion and brandishing a sword.',
	},
	{
		image: '../src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		title: 'Experience',
		subtitle: "Chef's Special",
		text: 'Our chef brings exquisite flavors, combining traditional techniques with modern twists. Each dish tells a story of passion and perfection, ensuring a unique dining experience for every guest.',
	},
	{
		image: '../src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		title: 'Ambiance',
		subtitle: 'Elegant Setting',
		text: 'Enjoy your meal in a beautifully designed interior, where every detail is crafted to create a warm and inviting atmosphere. From soft lighting to comfortable seating, we ensure a memorable dining experience.',
	},
];

const currentContent = ref(contents[0]);
let currentIndex = 0;
let interval = null;

const changeContent = (direction) => {
	const contentElements = document.querySelectorAll('.discover-title, .discover-img');
	contentElements.forEach(element => element.classList.add('fade-out'));

	setTimeout(() => {
		if (direction === 'left') {
			currentIndex = (currentIndex - 1 + contents.length) % contents.length; 
		} else {
			currentIndex = (currentIndex + 1) % contents.length; 
		}
		currentContent.value = contents[currentIndex];

		contentElements.forEach(element => element.classList.remove('fade-out'));
	}, 500); 
};

onMounted(() => {
	interval = setInterval(() => {
		changeContent('right');
	}, 5000); 
});

onUnmounted(() => {
	clearInterval(interval);
});
</script>

<style lang="scss" scoped>
.discover {
	width: 100%;
	position: relative;
	z-index: 3;
	background: var(--white);
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 25px;
	padding: 90px 150px;

	.discover-title,
	.discover-img {
		width: 50%;
		margin: 50px 0px;
		transition: opacity 0.5s ease-in-out; 
	}

	.discover-title {
		width: 100%;
		text-align: center;

		h3 {
			color: var(--primary);
			font-size: 48px;
			font-family: 'Playball', cursive;
		}

		.line {
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 30px;
			div {
				display: flex;
				align-items: center;
				flex-direction: column;
				gap: 5px;
				div {
					width: 30px;
					height: 1px;
					background: var(--primary);
				}
			}
			h5 {
				margin-top: 20px;
				font-size: 18px;
				text-transform: uppercase;
				font-weight: bold;
				padding-bottom: 20px;
				font-family: 'Source Sans Pro', sans-serif;
				color: var(--black);
			}
		}

		p {
			margin-top: 50px;
			text-align: left;
			font-size: 16px;
			line-height: 24px;
			padding-bottom: 10px;
			font-family: 'Source Sans Pro', sans-serif;
			color: var(--p-color);
		}

		.routerLink {
			text-decoration: none;
			text-align: left;
			font-size: 26px;
			font-weight: bold;
			color: var(--primary);
			font-family: 'Playball', cursive;
		}

		.angles {
			display: flex;
			align-items: center;
			position: absolute;
			top: 90%;
			width: 85%;
			justify-content: center;
			gap: 20px;

			.angles-left-btn, .angles-right-btn {
				background-color: transparent;
				border: none;
				color: var(--black);
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
		}
	}

	.discover-img {
		width: 80%;
		img {
			width: 100%;
			height: 100%;
			object-fit: cover;
		}
	}

	.discover-title.fade-out,
	.discover-img.fade-out {
		opacity: 0.5; 
	}
}
</style>
