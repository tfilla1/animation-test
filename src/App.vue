<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">animejs</div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/tfilla1/animation-test"
        target="_blank"
        text
      >
        <span class="mr-2">animation-test</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-card>
        <v-card-title>animation test</v-card-title>
        <v-card-text>
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
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn class="primary" @click="start">start</v-btn>
          <v-btn class="warning" @click="pause">pause</v-btn>
          <v-btn class="error" @click="stop">stop</v-btn>
        </v-card-actions>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import anime from "animejs";
export default {
  name: "App",
  data: () => ({
    animation: null,
    timeline: null,
  }),
  computed: {
    colors() {
      return ["#f0a", "#0af", "#a0f"];
    },
    targets() {
      return [".item", ".letter"];
    },
  },
  methods: {
    createTimeline() {
      this.timeline = anime.timeline({
        easing: "easeOutExpo",
        duration: 1500,
        loop: false,
      });
    },
    initialAnimation() {
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
          easing: "cubicBezier(.35,.94,.61,.27)",
          loop: true,
        })
        .add({
          targets: ".item",
          translateX: [250],
          opacity: 1,
          backgroundColor: ["#f0a", "#a0f", "#f0a"],
          duration: 1500,
          easing: "cubicBezier(.35,.94,.61,.27)",
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
        })
        .add({
          targets: ".item",
          translateX: [250, 150, 200],
          translateY: [0, 150, 190],
          width: [25, 75, 225],
          opacity: 1,
          backgroundColor: ["#f0a", "#a0f", "#f0a"],
          duration: 4000,
          easing: "cubicBezier(.35,.94,.61,.27)",
        });
    },
    start() {
      this.timeline.play();
    },
    pause() {
      this.timeline.pause();
    },
    stop() {
      this.timeline.stop();
    },
  },
  mounted() {
    this.createTimeline();
    this.initialAnimation();
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
