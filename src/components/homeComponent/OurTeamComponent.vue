<template>
	<section class="our-team">
		<div class="our-team-title">
			<h1 data-aos="zoom-in-up">Our Team</h1>
			<h3 data-aos="zoom-in-up">High-class professional service</h3>
			<p data-aos="zoom-in-up">
				Numerous commentators have also referred to the supposed restaurant
				owner's eccentric habit of touting for custom <br />
				outside his establishment, dressed in aristocratic fashion and
				brandishing a sword
			</p>
			<div class="bold-separator" data-aos="zoom-in-up">
				<div class="line"></div>
				<div class="dot"></div>
				<div class="line"></div>
			</div>

			<div class="about-chef">
				<div
					v-for="(item, index) in chefs"
					:key="index"
					@click="openModal(item)"
					class="chef-item group"
				>
					<img :src="item.img" alt="" data-aos="zoom-in-up" />
					<p class="info">{{ item.info }}</p>
					<div>
						<h4 data-aos="zoom-in-up">{{ item.name }}</h4>
						<p data-aos="zoom-in-up">{{ item.description }}</p>
					</div>
				</div>
			</div>

			<Transition>
				<div v-if="isOpen" class="chef-info">
					<div class="modal-content">
						<i @click="closeModal" class="fa-solid fa-xmark"></i>
						<div class="modal-info">
							<div class="img-box">
								<img class="chef-img" :src="selectedChef.img" alt="Chef Image" />
							</div>
							<div>
								<h4>{{ selectedChef.name }}</h4>
								<div class="modal-desc">
									<div class="modal-line"></div>
									<p class="chef-description">{{ selectedChef.description }}</p>
									<div class="modal-line"></div>
								</div>

								<p class="chef-information">{{ selectedChef.modal_desc }}</p>
								<div class="find-social">
									<h5>Finf on :</h5>
									<div class="networks">
										<a data-aos="zoom-in-up" href="#facebook"
											><i class="fa-brands fa-facebook-f"></i
										></a>
										<a
											data-aos="zoom-in-up"
											href="https://youtube.com/@yalovarestaurant?si=jaymsYgTnFntGGzI"
										>
											<i class="fa-brands fa-youtube"></i>
										</a>
										<a
											data-aos="zoom-in-up"
											href="https://www.instagram.com/yalova_restaurant?igsh=MWR4bmRhdzF5ZDJ2Mg=="
										>
											<i class="fa-brands fa-instagram"></i>
										</a>
										<a
											data-aos="zoom-in-up"
											href="https://t.me/yalova_restaurant"
										>
											<i class="fa-brands fa-telegram"></i>
										</a>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</Transition>
		</div>
	</section>
</template>

<script setup>
import { ref } from 'vue';
import chefImage from '/src/assets/shef.jpg';

const chefs = ref([
	{
		name: 'Andy Moro',
		description: 'Master chef in Brooklyn',
		img: chefImage,
		info: 'More info',
		modal_desc:
			'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat. Xillum dolore eu fugiat nulla pariatur. olore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
	},
	{
		name: 'Emily Smith',
		description: 'Pastry expert',
		img: chefImage,
		info: 'More info',
		modal_desc:
			'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat. Xillum dolore eu fugiat nulla pariatur. olore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
	},
	{
		name: 'John Doe',
		description: 'Grill master',
		img: chefImage,
		info: 'More info',
		modal_desc:
			'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat. Xillum dolore eu fugiat nulla pariatur. olore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
	},
	{
		name: 'Sarah Lee',
		description: 'Italian cuisine specialist',
		img: chefImage,
		info: 'More info',
		modal_desc:
			'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat. Xillum dolore eu fugiat nulla pariatur. olore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
	},
]);

const isOpen = ref(false);
const selectedChef = ref({});

const openModal = (chef) => {
	selectedChef.value = chef;
	isOpen.value = true;
};

const closeModal = () => {
	isOpen.value = false;
};
</script>

<style lang="scss" scoped>
.our-team {
	width: 100%;
	height: auto;
	position: relative;
	z-index: 3;
	background: var(--white);
	display: flex;
	place-items: center;
	text-align: center;
	padding: 100px 0px;

	.our-team-title {
		width: 100%;
		display: flex;
		flex-direction: column;
		place-items: center;
		color: var(--white);
		z-index: 2;

		h1 {
			width: 100%;
			color: var(--primary);
			text-transform: uppercase;
			font-weight: bold;
			font-size: 38px;
			letter-spacing: 6px;
			padding-bottom: 20px;
			font-family: 'Playball', cursive;
		}

		h3 {
			color: var(--black);
			font-size: 22px;
			font-family: 'Playball', cursive;
			margin-bottom: 40px;
		}

		p {
			text-align: center;
			font-size: 16px;
			line-height: 24px;
			padding-bottom: 10px;
			color: var(--p-color);
		}

		.bold-separator {
			text-align: center;
			display: flex;
			align-items: baseline;
			gap: 100px;
			margin: 50px 0px;

			.line {
				width: 130px;
				height: 1px;
				background: var(--primary);
			}

			.dot {
				width: 8px;
				height: 8px;
				background: var(--black);
				border-radius: 50%;
			}
		}

		.about-chef {
			width: 70%;
			margin-top: 30px;
			padding: 15px;
			display: grid;
			grid-template-columns: repeat(4, 1fr);
			place-items: center;

			.chef-item {
				display: flex;
				flex-direction: column;
				align-items: center;
				gap: 5px;
				cursor: pointer;
				transition: 1s;

				img {
					width: 80%;
					height: 80%;
					border-radius: 50%;
					object-fit: cover;
					position: relative;
				}

				.info {
					font-size: 24px;
					font-weight: bold;
					letter-spacing: 1px;
					font-family: 'Playball', cursive;
					color: var(--black);
					position: absolute;
					padding-top: 6%;
					opacity: 0;
					transition: 1s;
				}

				div {
					h4 {
						font-size: 18px;
						font-weight: bold;
						letter-spacing: 1px;
						font-family: 'Playball', cursive;
						color: var(--black);
					}

					p {
						font-size: 14px;
						font-weight: bold;
						color: var(--primary);
						font-family: 'Source Sans Pro', sans-serif;
					}
				}
			}

			.chef-item:hover {
				opacity: 50%;
			}

			.group {
				&:hover {
					.info {
						opacity: 100%;
					}
				}
			}
		}
	}

	.chef-info {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}

	.modal-content {
		background: var(--white);
		padding: 20px;
		border-radius: 10px;
		text-align: center;
		width: 50%;
		position: relative;

		.modal-info {
			display: flex;
			justify-content: center;
			align-items: center;
			gap: 40px;

			.img-box {
				object-fit: cover;
				position: relative;
			}

			.modal-desc {
				display: flex;
				justify-content: space-between;
				align-items: center;
			}

			.modal-line {
				width: 50px;
				height: 1px;
				background: var(--primary);
			}

			.chef-description {
				font-size: 20px;
				font-weight: bold;
				color: var(--black);
				font-family: 'Source Sans Pro', sans-serif;
			}

			.chef-information {
				font-size: 14px;
				font-weight: medium;
				color: var(--black);
				font-family: 'Source Sans Pro', sans-serif;
			}

			h4 {
				font-size: 35px;
				font-weight: bold;
				letter-spacing: 1px;
				font-family: 'Playball', cursive;
				color: var(--primary);
				margin-bottom: 10px;
			}

			.find-social {
				h5 {
					font-size: 18px;
					font-weight: bold;
					letter-spacing: 1px;
					font-family: 'Playball', cursive;
					color: var(--primary);
					margin-bottom: 10px;
				}
				.networks {
					display: flex;
					gap: 15px;
					justify-content: center;

					a {
						color: var(--black);

						&:hover {
							color: var(--primary);
						}
					}
				}
			}
		}
	}

	.fa-xmark {
		position: absolute;
		top: 10px;
		right: 10px;
		cursor: pointer;
		font-size: 24px;
		color: var(--black);
	}

	@media screen and (max-width: 1450px) {
		.our-team-title {
			.about-chef {
				width: 90%;
			}

			
		}
	}

	@media screen and (max-width: 1293px) {
		.our-team-title {
			.chef-info {
				padding: 100px;
			}
			.modal-info {
				display: inline-block;
			}

			.img-box {
				display: flex;
				justify-content: center;
				margin-bottom: 20px;

				img {
					width: 50%;
				}
			}
		}
	}

	@media screen and (max-width: 1000px) {
		.our-team-title {
			.modal-info {
				h4 {
					font-size: 22px;
				}

				.chef-description {
					font-size: 18px;
				}

				.chef-information {
					font-size: 11px;
				}
			}
		}
	}

	@media screen and (max-width: 776px) {
		.our-team-title {
			.about-chef {
				width: 90%;
				display: grid;
				grid-template-columns: repeat(2, 1fr);
			}

			.chef-info{
				.modal-content {
					width: 500px;
				}
			}
		}
	}

	@media screen and (max-width: 576px) {
		.our-team-title {
			h1 {
				font-size: 28px;
			}

			h3 {
				font-size: 18px;
			}

			a {
				font-size: 22px;
			}

			.bold-separator {
				gap: 30px;
			}

			.about-chef {
				width: 90%;
				display: grid;
				grid-template-columns: repeat(1, 1fr);
			}


			.img-box {
				img {
					width: 80%;
				}
			}
		}
	}
}
</style>
