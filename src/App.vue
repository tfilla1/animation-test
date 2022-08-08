<template>
  <div id="app">
    <!-- <h1>
      <span class="letter">h</span>
      <span class="letter">e</span>
      <span class="letter">l</span>
      <span class="letter">l</span>
      <span class="letter">o</span>
    </h1> -->
    <button @click="start">start</button>
    <button @click="pause">pause</button>
    <div class="wrapper">
      <div class="item"></div>
      <h1>
        <span class="letter pa-1">h</span>
        <span class="letter pa-1">e</span>
        <span class="letter pa-1">l</span>
        <span class="letter pa-1">l</span>
        <span class="letter pa-1">o</span>
      </h1>
    </div>
    <br />
  </div>
</template>

<script>
import anime from "animejs";
export default {
  name: "App",
  data: () => ({
    animation: null,
    timeline: null,
  }),
  methods: {
    start() {
      this.animation.play();
    },
    pause() {
      this.animation.pause();
    },
  },
  mounted() {
    // this.animation = anime({
    //   targets: ".letter",
    //   backgroundColor: ["#f0a", "#af0", "#f0a"],
    //   scale: [1, 2, 1],
    // });
    // this.animation = anime({
    //   targets: ".letter",
    //   color: ["#ff0", "#0ff", "#ff0"],
    //   top: 0,
    //   left: 0,
    //   opacity: 1,
    //   translateX: [0, 10],
    //   translateY: [0, 150],
    //   rotate: {
    //     value: 1080,
    //     duration: 2000,
    //     easing: "easeOutExpo",
    //   },
    //   scale: anime.stagger([1, 2, 1], { from: "center" }),
    //   delay: anime.stagger(1000, { start: 0 }),
    //   loop: true,
    // });

    this.timeline = anime.timeline({
      easing: "easeOutExpo",
      duration: 1500,
      loop: true,
    });

    this.timeline
      .add({
        targets: ".item",
        backgroundColor: ["#f0a", "#0af", "#a0f", "#0af", "#f0a"],
        translateY: [0, 250, 450, 250, 0],
        translateX: [0, 250, 450, 250, 0],
        rotate: [0, 180, 0, 180, 0],
        opacity: 1,
        duration: 3500,
        scale: [1, 4, 1, 4, 1],
        easing: 'cubicBezier(.35,.94,.61,.27)',
        loop: true,
      })
      .add({
        targets: ".item",
        translateX: [250],
        opacity: 1,
        backgroundColor: ["#f0a", "#a0f", "#f0a"],
        duration: 1500,
        easing: 'cubicBezier(.35,.94,.61,.27)'
      })
      .add({
        targets: ".letter",
        color: ["#ff0", "#0ff", "#ff0"],
        top: 0,
        left: 0,
        opacity: 1,
        translateX: [0, 10],
        translateY: [0, 150],
        rotate: {
          value: 1080,
          duration: 2000,
          easing: "easeOutExpo",
        },
        scale: anime.stagger([1, 2, 1], { from: "center" }),
        delay: anime.stagger(1000, { start: 0 }),
        loop: true,
      })
      .add({
        targets: ".item",
        translateX: [0],
        translateY: [0, 250, 0],
        opacity: 1,
        backgroundColor: ["#f0a", "#a0f", "#f0a"],
        duration: 4000,
        easing: 'cubicBezier(.35,.94,.61,.27)'
      });
  },
};
</script>

<style>
.letter {
  display: inline-block;
  opacity: 0;
  top: 0;
  left: 0;
}
.d-none {
  display: none;
}
.pa-1 {
  padding: 15px;
}
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
