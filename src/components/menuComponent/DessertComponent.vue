<template>
  <div class="dessert">
    <div class="overlay"></div>
    <div class="dessert-title">
      <h1 data-aos="zoom-in-up">Dessert</h1>
      <p data-aos="zoom-in-up">Aenean ultricies mi vitae est</p>
    </div>
  </div>

  <div id="tushlik" class="hot-dishes">
    <h2 data-aos="zoom-in-up" class="font-bold text-3xl mb-10 font-[Playball,cursive] text-[var(--primary)]">Tushlik</h2>
		<div class="menu-item-box">
			<div
				data-aos="zoom-in-up"
				class="menu-item"
				v-for="(item, idx) in menuItems"
				:key="idx"
			>
				<div class="menu-item-title">
          <div class="flex justify-center">
            <img
              @click.prevent="openModal(idx)"
              class="max-w-[300px] rounded-lg cursor-pointer"
              :src="item.img"
            />
          </div>
          <div class="line"></div>
					<h5>{{ item.price }}</h5>
				</div>
				<p class="text-center md:text-start">{{ item.description }}</p>
			</div>
		</div>

		<div v-if="isModalOpen" class="relative overflow-hidden">
			<div class="fixed inset-0 w-full h-full flex justify-center items-center">
				<div
					class="relative rounded-lg md:max-h-[100vh] lg:max-w-[100%] lg:max-h-[80%] bg-white opacity-90 z-10 p-20"
				>
					<button
						@click="closeModal"
						class="relative left-[100%] bottom-[0px] text-[var(--black)] cursor-pointer hover:opacity-50"
					>
						<i class="fa-solid fa-xmark fa-2xl"></i>
					</button>

					<div class="flex justify-center gap-10 text-[var(--primary)] font-bold text-2xl mb-5">
						<button class="cursor-pointer" @click="isVideo = false">Photo</button>
						<button class="cursor-pointer" @click="isVideo = true">Video</button>
					</div>

					<div class="flex justify-between items-center gap-5 sm:gap-10 md:gap-30 lg:gap-40">
						<button @click="previousImage" class="text-4xl text-[var(--primary)] cursor-pointer active:opacity-50">
							<i class="fa-solid fa-angle-left"></i>
						</button>

						<div class="flex justify-center">
							<video v-if="isVideo" controls class="transition-all duration-500 w-[100%] lg:h-[500px] object-cover rounded-lg">
								<source :src="menuItems[currentIndex].video" type="video/mp4" />
								Your browser does not support the video tag.
							</video>

							<img v-else :src="menuItems[currentIndex].img" class="transition-all duration-500 w-[100%] lg:h-[500px] object-cover rounded-lg" />
						</div>

						<button @click="nextImage" class="text-4xl text-[var(--primary)] cursor-pointer active:opacity-50">
							<i class="fa-solid fa-angle-right"></i>
						</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';

const menuItems = ref([
	{
		img: 'src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		video: 'http://lambert.kwst.net/site/video/1.mp4',
		description: 'Labore et dolore',
		price: '$34',
	},
	{
		img: 'src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		video: 'http://lambert.kwst.net/site/video/1.mp4',
		description: 'Semonstraverunt',
		price: '$130',
	},
	{
		img: 'src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		video: 'http://lambert.kwst.net/site/video/1.mp4',
		description: 'Incididunt ut labore',
		price: '$30',
	},
	{
		img: 'src/assets/jason-leung-poI7DelFiVA-unsplash.jpg',
		video: 'http://lambert.kwst.net/site/video/1.mp4',
		description: 'Adipisicing elit',
		price: '$61',
	},
]);

const isModalOpen = ref(false);
const currentIndex = ref(0);
const isVideo = ref(false);

const openModal = (index) => {
	currentIndex.value = index;
	isModalOpen.value = true;
	isVideo.value = false; 
};

const closeModal = () => {
	isModalOpen.value = false;
};

const previousImage = () => {
	currentIndex.value = (currentIndex.value - 1 + menuItems.value.length) % menuItems.value.length;
	isVideo.value = false; 
};

const nextImage = () => {
	currentIndex.value = (currentIndex.value + 1) % menuItems.value.length;
	isVideo.value = false;
};
</script>

<style lang="scss" scoped>
.dessert {
  width: 100%;
  height: 65vh;
  position: relative;
  z-index: 3;
  background-image: url("../../assets/jason-leung-poI7DelFiVA-unsplash.jpg");
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  background-repeat: no-repeat;
  display: flex;
  place-items: center;
  text-align: center;

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
    opacity: 0.6;
  }

  .dessert-title {
    width: 100%;
    z-index: 3;

    h1 {
      width: 100%;
      font-size: 3.5em;
      margin-bottom: 10px;
      color: var(--white);
      font-weight: bold;
      letter-spacing: 3px;
      font-family: "Source Sans Pro", sans-serif;
    }

    p {
      font-size: 34px;
      font-family: "Playball", cursive;
      color: var(--primary);
    }
  }
}

.hot-dishes {
	width: 100%;
	position: relative;
	z-index: 3;
	background: var(--white);
	padding: 100px 150px;
	color: black;
	display: flex;
	flex-direction: column;
	place-items: center;

	.menu-item-box {
		width: 100%;
		display: grid;
		place-items: center;
		grid-template-columns: repeat(2, 1fr);
		gap: 60px;
		margin: 50px;

		.menu-item {
			display: flex;
			flex-direction: column;
			gap: 5px;
			width: 100%;

			.menu-item-title {
				display: flex;
				align-items: center;
				justify-content: space-between;
				gap: 30px;

				.line {
					width: 75%;
					border: 1px dotted var(--primary);
				}

				h5 {
					font-size: 20px;
					font-weight: 400;
					font-family: 'Source Sans Pro', sans-serif;
				}
			}

			p {
				font-size: 16px;
				color: var(--p-color);
				font-family: 'Source Sans Pro', sans-serif;
			}
		}
	}

	.bold-separator {
		width: auto;
		display: flex;
		place-items: center;
		align-items: baseline;
		gap: 100px;
		margin-top: 50px;

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
}
@media screen and (max-width: 1450px) {
	.hot-dishes {
		padding: 100px 30px;
	}
}

@media screen and (max-width: 992px) {
	.hot-dishes {
		.menu-item-box {
			display: grid;
			grid-template-columns: repeat(1, 1fr);
		}
	}
}

@media screen and (max-width: 776px) {
	.hot-dishes {
		.menu-item-box {
			.menu-item {
				.menu-item-title {
          display: inline-block;
          text-align: center;

          .line {
            display: none;
          }
					h5 {
						font-size: 14px;
            margin-top: 10px;
					}
				}
				p {
					font-size: 12px;
				}
			}
		}

		.bold-separator {
			gap: 30px;
		}
	}
}

@media screen and (max-width: 576px) {
	.hot-dishes {
		.bold-separator {
			gap: 30px;
		}
	}
}

@media screen and (max-width: 576px) {
  .dessert {
    .dessert-title {
      h1 {
        font-size: 32px;
      }

      p {
        font-size: 22px;
      }
    }
  }
}
</style>
