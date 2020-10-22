<template>
  <div id="app">
    <Game/>
  </div>
</template>

<script>
import Game from './components/Game'

export default {
  name: 'App',
  components: {
    Game
  }
}
</script>

<style>
  @import url(https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.0/normalize.min.css);
  *, *:after, *:before {
    box-sizing: border-box;
  }

  body, html, #app {
    height: 100%;
  }

  @font-face {
    font-family: 'zig';
    src: url('./assets/zig.ttf');
  }
</style>
