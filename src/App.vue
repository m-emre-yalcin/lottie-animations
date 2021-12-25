<template>
  <div id="app">
    <div class="animation-box">
      <lottie
        :options="defaultOptions"
        :height="400"
        :width="400"
        v-on:animCreated="handleAnimation"
      />
      <div>
        <p>Speed: x{{ animationSpeed }}</p>
        <input
          type="range"
          value="1"
          min="0"
          max="3"
          step="0.5"
          v-on:change="onSpeedChange"
          v-model="animationSpeed"
        />
      </div>
      <button v-on:click="stop">stop</button>
      <button v-on:click="pause">pause</button>
      <button v-on:click="play">play</button>
    </div>
  </div>
</template>

<script>
import Lottie from "vue-lottie";
export default {
  components: {
    lottie: Lottie,
  },
  data() {
    return {
      defaultOptions: {
        animationData: require("../data/mp4tojson.json"),
        autoplay: false,
        loop: true,
      },
      animationSpeed: 0.25,
      anim: null,
    };
  },
  methods: {
    handleAnimation: function (anim) {
      this.anim = anim;
    },
    stop: function () {
      this.anim.stop();
    },
    play: function () {
      this.anim.play();
    },
    pause: function () {
      this.anim.pause();
    },
    onSpeedChange: function () {
      this.anim.setSpeed(this.animationSpeed);
    },
    onScroll: function () {
      console.log(window.scrollY);
      this.anim.goToAndStop(window.scrollY * 2);
    },
  },
  mounted() {
    document.addEventListener("scroll", this.onScroll);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 200vh;
}
.animation-box {
  position: sticky;
  top: 10px;
}
</style>
