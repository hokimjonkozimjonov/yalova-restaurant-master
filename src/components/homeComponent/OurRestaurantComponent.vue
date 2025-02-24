<template>
	<section class="our-restaurant">
		<div class="our-restaurant-img" data-aos="zoom-in-up">
			<img :src="currentContent.image" alt="ourRestaurant.img"/>
		</div>
		<div class="our-restaurant-title">
			<h3 data-aos="zoom-in-up">  {{ currentContent.title }}</h3>
			<div class="line" data-aos="zoom-in-up">
				<div>
					<div></div>
					<div></div>
				</div>
				<h5> {{ currentContent.subtitle }} </h5>
				<div>
					<div></div>
					<div></div>
				</div>
			</div>
			<p data-aos="zoom-in-up">
				{{ currentContent.text }}
			</p>
			<RouterLink class="routerLink" to="/gallery">
				<h4 data-aos="zoom-in-up">View Gallery</h4>
			</RouterLink>
		</div>

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
	</section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const contents = [
	{
		image: '../src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		title: 'Our restaurant',
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
.our-restaurant {
	width: 100%;
	position: relative;
	z-index: 3;
	background: var(--white);
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 25px;
	padding: 90px 150px;

	.our-restaurant-title,
	.our-restaurant-img {
		width: 50%;
		margin: 50px 0px;
	}

	.our-restaurant-title {
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

		h4 {
			text-align: left;
			font-size: 26px;
			font-weight: bold;
			color: var(--primary);
			font-family: 'Playball', cursive;
		}

		.routerLink {
			text-decoration: none;
			text-align: left;
			font-size: 26px;
			font-weight: bold;
			color: var(--primary);
			font-family: 'Playball', cursive;
		}
	}

	.our-restaurant-img {
		width: 80%;
		img {
			width: 100%;
			height: 100%;
			object-fit: cover;
		}
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

@media screen and (max-width: 1450px) {
	.our-restaurant {
		padding: 50px 20px;
	}
}

@media screen and (max-width: 992px) {
	.our-restaurant {
		display: flex;
		flex-direction: column;

		.our-restaurant-title,
		.our-restaurant-img {
			margin: 30px 0px;
		}

		.our-restaurant-img {
			width: 100%;
			margin-top: 70px;
		}
	}
}

@media screen and (max-width: 576px) {
	.our-restaurant {
		.our-restaurant-title {
			h3 {
				font-size: 28px;
			}
		}
	}
}
</style>
