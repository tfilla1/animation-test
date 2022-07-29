<template>
  <div id="app">
    <button @click="start">start</button>
    <button @click="pause">pause</button>
    <div class="wrapper">
      <div class="item">
        <span class="letter">hello</span>
      </div>
    </div>
  </div>
</template>

<script>
import anime from 'animejs';
export default {
  name: 'App',
  data: () => ({
    animation: null,
    letter: null
  }),
  methods: {
    start() {
      this.animation.play();
    },
    pause() {
      this.animation.pause();
    }
  },
  mounted() {
    this.animation = anime({
      targets: '.item',
      backgroundColor: ['#f0a', '#0af', '#a0f', '#0af', '#f0a'],
      translateY: [0, 250, 450, 250, 0],
      translateX: [0, 250, 450, 250, 0],
      rotate: [0, 50, 0, 75, 0],
      duration: 3500,
      scale: [1, 2, 1, 2, 1],
      text: ['', 'hi', ''],
      loop: true
    });

    this.letter = anime({
      targets: '.letter',
      
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.wrapper {
  background-color: #000;
  width: 500px;
  height: 500px;
}
.item {
  background-color: #ff00aa;
  width: 50px;
  height: 50px;
}
</style>
