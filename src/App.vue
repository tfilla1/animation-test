<template>
  <div id="app">
    <v-app>
      <v-app-bar app color="primary" dark>
        <div class="d-flex align-center">animejs</div>
        <v-btn text to="/">Home</v-btn> |
        <v-btn text to="/about">About</v-btn>
        <v-btn text to="/animations">animations</v-btn>

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
        <router-view />
      </v-main>
    </v-app>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
