<template>
  <footer>
    <div class="about">
      <div class="about-us">
        <h3 data-aos="zoom-in-up">About Us</h3>
        <p data-aos="zoom-in-up">
          Numerous commentators have also referred to the supposed restaurant
          owner's eccentric habit of touting for custom outside his
          establishment, dressed in aristocratic fashion and brandishing a sword
        </p>
      </div>
      <div class="find-us">
        <h3 data-aos="zoom-in-up">Find Us</h3>
        <div>
          <a data-aos="zoom-in-up" href="#facebook">
            <i class="fa-brands fa-facebook-f"></i>
          </a>
          <a data-aos="zoom-in-up" href="https://youtube.com/@yalovarestaurant?si=jaymsYgTnFntGGzI">
            <i class="fa-brands fa-youtube"></i>
          </a>
          <a data-aos="zoom-in-up" href="https://www.instagram.com/yalova_restaurant?igsh=MWR4bmRhdzF5ZDJ2Mg==">
            <i class="fa-brands fa-instagram"></i>
          </a>
          <a data-aos="zoom-in-up" href="https://t.me/yalova_restaurant">
            <i class="fa-brands fa-telegram"></i>
          </a>
        </div>
      </div>
    </div>

    <div class="footer-contact">
      <div class="bold-separator" data-aos="zoom-in-up">
        <div class="line"></div>
        <div class="dot"></div>
        <div class="line"></div>
      </div>

      <ul>
        <a href="tel:+998712052255"><li data-aos="zoom-in-up">+998 (71) 205 22 55</li></a>
        <a href="https://maps.apple.com/?ll=41.297354,69.243272&q=41.297353521898714,69.24327186141528&t=m"><li data-aos="zoom-in-up">Burijar street 1, Tashkent, Uzbekistan</li></a>
        <a href="#"><li data-aos="zoom-in-up">yourmail@domain.com</li></a>
      </ul>
    </div>
  </footer>
  <div class="tap-top-holder">
    <div class="container">
      <div>
        <p data-aos="zoom-in-up">© Yalova 2015 .</p>
        <span data-aos="zoom-in-up"> All rights reserved.</span>
      </div>
      <a @click="scrollToTop" class="cursor-pointer active:opacity-50 hover:opacity-70">
        <p data-aos="zoom-in-up">Back To Top</p>
      </a>
      
    </div>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();

const scrollToTop = () => {
  if (route.path === "/") {
    window.scrollTo({ top: 0, behavior: "smooth" });
  } else {
    router.push({ path: route.path, hash: "#top" });
  }
};
</script>

<style lang="scss" scoped>
footer {
  position: relative;
  z-index: 3;
  background: var(--footer-bg);
  width: 100%;
  padding: 90px 0px;

  .about {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0px 150px;

    .about-us {
      width: 50%;
      h3 {
        text-align: center;
        width: 100%;
        color: var(--white);
        font-size: 20px;
        text-transform: uppercase;
        font-weight: bold;
        letter-spacing: 1px;
        margin-bottom: 40px;
        font-family: "Source Sans Pro", sans-serif;
      }

      p {
        text-align: center;
        font-size: 16px;
        font-family: "Playball", cursive;
        color: var(--footer-p-color);
      }
    }

    .find-us {
      h3 {
        text-align: center;
        font-family: "Playball", cursive;
        font-size: 22px;
        margin-bottom: 50px;
        color: var(--primary);
      }

      div {
        display: flex;
        align-items: center;
        gap: 25px;
        a {
          color: var(--white);

          &:hover {
            color: var(--primary);
          }
        }
      }
    }
  }
  @media screen and (max-width: 768px) {
    .about {
      display: flex;
      flex-direction: column;
      width: 100%;
      .about-us,
      .find-us {
        margin-top: 50px;
        width: 100%;
        display: flex;
        flex-direction: column;
        place-items: center;
      }
    }
  }

  .footer-contact {
    margin-top: 50px;
    width: 100%;
    display: grid;
    place-items: center;

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
        background: var(--white);
        border-radius: 50%;
      }
    }

    ul {
      display: flex;
      align-items: center;
      gap: 25px;

      div {
        width: 5px;
        height: 5px;
        background: var(--footer-p-color);
        border-radius: 50%;
      }

      a {
        text-decoration: none;
      }

      li {
        color: var(--footer-p-color);
        font-size: 15px;
        font-weight: 500;
        font-family: "Source Sans Pro", sans-serif;
        list-style: none;
      }

      li:not(:first-child) {
        list-style: disc;
      }
    }
  }

  @media screen and (max-width: 1450px) {
    .about {
      padding: 20px;
    }
  }

  @media screen and (max-width: 576px) {
    .footer-contact .bold-separator {
      gap: 50px;
      width: 100%;
      padding: 20px;

      .line {
        width: 50%;
      }
    }

    .footer-contact ul {
      display: flex;
      flex-direction: column;
    }
  }
}

.tap-top-holder {
  position: relative;
  z-index: 3;
  background: var(--footer-holder-bg);
  width: 100%;
  .container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 30px 150px;

    div {
      display: flex;
      align-items: center;
      gap: 13px;

      p {
        color: var(--primary);
        font-size: 16px;
        font-family: "Playball", cursive;
      }

      span {
        color: (--white);
        font-size: 16px;
        font-family: "Playball", cursive;
      }
    }
    p {
      color: var(--primary);
      font-size: 16px;
      font-family: "Playball", cursive;
    }
  }

  @media screen and (max-width: 1450px) {
    .container {
      padding: 20px 50px;
    }
  }

  @media screen and (max-width: 576px) {
    .container {
      display: flex;
      flex-direction: column;
    }
  }

  @media screen and (max-width: 376px) {
    .container {
      div {
        display: flex;
        flex-direction: column;
      }
    }
  }
}
</style>
