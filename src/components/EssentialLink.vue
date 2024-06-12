<template>
  <div class="slideshow">
    <div class="slides">
      <div
        v-for="(slide, index) in slides"
        :key="index"
        :class="['slide', { active: index === currentIndex }]"
      >
        <img :src="slide" alt="Slide Image" />
      </div>
    </div>
    <div class="controls">
      <button @click="prevSlide">Previous</button>
      <button @click="nextSlide">Next</button>
    </div>
    <div class="indicators">
      <span
        v-for="(slide, index) in slides"
        :key="index"
        :class="['indicator', { active: index === currentIndex }]"
        @click="goToSlide(index)"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      slides: [
        require("@/assets/slide1.jpg"),
        require("@/assets/slide2.jpg"),
        require("@/assets/slide3.jpg"),
        // Add more image paths as needed
      ],
      currentIndex: 0,
      autoPlayInterval: null,
    };
  },
  methods: {
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
    },
    prevSlide() {
      this.currentIndex =
        (this.currentIndex - 1 + this.slides.length) % this.slides.length;
    },
    goToSlide(index) {
      this.currentIndex = index;
    },
    startAutoPlay() {
      this.autoPlayInterval = setInterval(this.nextSlide, 3000);
    },
    stopAutoPlay() {
      clearInterval(this.autoPlayInterval);
    },
  },
  mounted() {
    this.startAutoPlay();
  },
  beforeUnmount() {
    this.stopAutoPlay();
  },
};
</script>

<style>
.slideshow {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: auto;
  overflow: hidden;
}

.slides {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.slide {
  min-width: 100%;
  transition: opacity 1s;
}

.slide img {
  width: 100%;
  display: block;
}

.slide:not(.active) {
  display: none;
}

.controls {
  display: flex;
  justify-content: space-between;
  position: absolute;
  top: 50%;
  width: 100%;
  transform: translateY(-50%);
}

.indicators {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 10px;
  width: 100%;
}

.indicator {
  width: 10px;
  height: 10px;
  margin: 0 5px;
  background-color: #ccc;
  border-radius: 50%;
  cursor: pointer;
}

.indicator.active {
  background-color: #333;
}
</style>
