<template>
  <v-container>
    <v-row>
      <v-col cols="6">
        <v-card>
          <v-card-title>animation test</v-card-title>
          <v-card-text>
            <v-form v-model="valid" ref="form">
              <v-select
                label="targets"
                v-model="animation.targets"
                :items="targets"
                :rules="targetRules"
              ></v-select>
              <v-select
                label="color"
                v-model="animation.color"
                :items="colors"
              ></v-select>
              <v-select
                label="background color"
                v-model="animation.backgroundColor"
                :items="backgroundColors"
              ></v-select>
              <v-btn class="mr-4" color="success" text @click="newAnimation"
                >new animation</v-btn
              >
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn class="primary" @click="start">start</v-btn>
            <v-btn class="warning" @click="pause">pause</v-btn>
            <v-btn class="error" @click="restart">restart</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
      <v-col cols="6">
        <div class="item"></div>
        <h1>
          <span class="letter pa-1">h</span>
          <span class="letter pa-1">e</span>
          <span class="letter pa-1">l</span>
          <span class="letter pa-1">l</span>
          <span class="letter pa-1">o</span>
        </h1>
      </v-col>
      <v-col cols="6">
        <v-card>
          <v-card-text>
            <code>{{ this.timeline }}</code>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
const STARTING_WIDTH = 50;
const STARTING_HEIGHT = 50;
const STARTING_DURATION = 1500;

const newAnimation = () => ({
  targets: "",
  rotate: 0,
  translateX: 0,
  translateY: 0,
  color: "",
  backgroundColor: "",
  easing: "",
  opacity: "",
  duration: STARTING_DURATION,
  scale: 0,
  loop: true,
  width: STARTING_WIDTH,
  height: STARTING_HEIGHT,
});


import anime from "animejs";
export default {
  name: "App",
  data: () => ({
    animation: anime(newAnimation()),
    timeline: null,
    valid: true,
    targetRules: [(v) => !!v || "Target is required"],
  }),
  computed: {
    colors() {
      return ["#f0a", "#0af", "#a0f", undefined];
    },
    backgroundColors() {
      return ["#f0a", "#0af", "#a0f", undefined];
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
        loop: true,
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
    newAnimation() {
        console.log(this.animation.targets);
        this.timeline.add(anime(this.animation));
        // this.timeline.add({
        //   targets: '.item',
        //   backgroundColor: this.animation.backgroundColor,
        //   color: this.animation.color,
        //   duration: STARTING_DURATION,
        // });
    },
    start() {
      this.timeline.play();
    },
    pause() {
      this.timeline.pause();
    },
    restart() {
      this.timeline.restart();
    },
  },
  mounted() {
    this.createTimeline();

    //this.initialAnimation();
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
.item {
  background-color: #ff00aa;
  width: 50px;
  height: 50px;
}
</style>
