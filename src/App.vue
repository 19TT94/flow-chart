<template>
  <div id="app">
    <wrapper target="#app" />

    <h1 class="page-title">
      Flow Chart Demo
    </h1>

    <grid />

    <a
      class="github"
      href="https://github.com/19TT94/flow-chart"
      target="_blank"
    >
      <img src="@/assets/github.png">
    </a>

  </div>
</template>

<script>

import Grid from './components/Grid.vue'
import Wrapper from './components/Wrapper.vue';

export default {
  name: 'app',

  components: {
    Grid,
    Wrapper
  }
}
</script>

<style lang="scss">

@import '@/assets/scss/core/all.scss';

$app: #f2e7c9;

#app {
  position: relative;
  color: #2c3e50;
  margin-top: 60px;
  background-color: $app;
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 10px;
  display: flex;
  flex-direction: column;

  .page-title {
    font-size: 40px;
    padding: $pad;
  }

  .github {
    position: absolute;
    bottom: 0;
    left: 0;
    padding: $pad;

    img {
      width: 20px;
      height: 20px;
    }
  }
}
</style>
