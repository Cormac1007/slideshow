<template>
  <div id="app">
    <div class="logo">
      <img src="./assets/logo(3).jpeg" alt="Logo" />
    </div>
    <div class="slideshow">
      <div
        v-for="(image, index) in images"
        :key="index"
        :class="['slide', { active: index === activeIndex }]"
        :style="{ backgroundImage: 'url(' + image + ')' }"
      ></div>
    </div>
    <p class="text">Mersvo</p>
  </div>
</template>

<script>
import img1 from "./assets/alister.jpeg";
import img2 from "./assets/meme.jpeg";
import img3 from "./assets/marble.jpeg";
import img4 from "./assets/bias.jpeg";

export default {
  name: "App",
  data() {
    return {
      images: [img1, img2, img3, img4],
      activeIndex: 0,
    };
  },
  mounted() {
    this.startSlideshow();
  },
  methods: {
    startSlideshow() {
      setInterval(() => {
        this.activeIndex = (this.activeIndex + 1) % this.images.length;
      }, 10000); // Switch every 10 seconds
    },
  },
};
</script>

<style>
#app {
  position: relative;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.logo {
  position: absolute;
  top: 10px;
  left: 10px;
}

.logo img {
  width: 300px; /* Adjust the size of the logo as needed */
  height: auto;
}

.slideshow {
  width: 60%; /* Adjust the width as needed */
  height: 60%; /* Adjust the height as needed */
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.slide {
  width: 100%; /* Make the slide take full width of the slideshow container */
  height: 100%; /* Make the slide take full height of the slideshow container */
  background-size: contain; /* Use contain to maintain aspect ratio */
  background-position: center;
  background-repeat: no-repeat; /* Ensure the image doesn't repeat */
  opacity: 0;
  transition: opacity 1s ease-in-out;
  position: absolute; /* Position absolute to overlap slides */
}

.slide.active {
  opacity: 1;
}

.text {
  position: absolute;
  bottom: 10px;
  left: 10px;
  color: red;
  font-size: 70px;
  z-index: 10;
}
</style>
