<template>
  <div class="background">
    <img src="./assets/moon.png" class="moon">
    <img
      :src="cloudOneImg"
      v-for="(cloud, index) in clouds"
      :key="index"
      class="cloud"
      :style="{ top: cloud.top + 'px', animationDelay: cloud.delay + 's' }"
      @animationend="onAnimationEnd"
    >
    <img
      :src="cloudTwoImg"
      v-for="(cloud, index) in clouds"
      :key="index"
      class="cloud"
      :style="{ top: cloud.top*Math.floor(Math.random() * 2) + 'px', animationDelay: cloud.delay + 's' }"
      @animationend="onAnimationEnd"
    >
  </div> 
</template>

<script>
import cloud from "./assets/cloud.png"
import cloud1 from "./assets/cloud1.png"
import cloud2 from "./assets/cloud2.png"
import cloud3 from "./assets/cloud3.png"
import cloud4 from "./assets/cloud4.png"

export default {
  data() {
    return {
      clouds: [],
      cloudImages: [cloud, cloud1, cloud2, cloud3, cloud4],
      cloudOneImg: null,
      cloudTwoImg: null, 
      offset: 0,
    };
  },
  mounted() {
    this.generateClouds();
    this.generateTopOffset();
    this.cloudOneImg = this.getRandomImage();
    this.cloudTwoImg = this.getRandomImage();
  },
  methods: {
    getRandomImage() {
      return this.cloudImages[Math.floor(Math.random() * this.cloudImages.length)];
    },
    generateClouds() {
      this.clouds = Array.from({ length: 4 }, (_, index) => ({
        top: Math.floor(Math.random() * 200),
        delay: index * 7,
      }));
    },
    onAnimationEnd() {
      this.generateClouds();
      this.generateTopOffset();
    },
    generateTopOffset() {
      this.offset = Math.floor(Math.random() * 2);
    }
  },
};

</script>

<style>

.background {
  background-color: #0a033e;
  color: white;
  text-align: center;
  height: 100vh;
}

.moon {
  height: 500px;
  filter: blur(2px);
  -webkit-filter: blur(2px);
}

.cloud {
  position: absolute;
  height: 500px;
  opacity: 0.5;
  left: -100%;
  animation: slide-in-cloud 15s linear infinite;
}

@keyframes slide-in-cloud {
  0% {
    left: -100%; 
  }
  50% {
    left: 0; 
  }
  100% {
    left: 100%; 
  }
}

</style>
