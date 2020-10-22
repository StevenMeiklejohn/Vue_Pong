<template>
  <div id="game" ref="game">
    <div id="centerLine"></div>
    <Scoreboard :playerOneScore="playerOneScore" :playerTwoScore="playerTwoScore" />
    <Ball @goal="handleGoal" />
    <PaddleLeft isLeftPaddle />
    <PaddleRight />
  </div>
</template>
<script>
import Scoreboard from './Scoreboard'
import Ball from './Ball'
import PaddleLeft from './PaddleLeft'
import PaddleRight from './PaddleRight'
export default {
  name: 'Game',
  components: {
    Scoreboard,
    Ball,
    PaddleLeft,
    PaddleRight
  },
  data () {
    return {
      playerOneScore: 0,
      playerTwoScore: 0
    }
  },
  methods: {
    handleGoal (player) {
      if (player === 'playerOne') {
        this.playerOneScore++
      } else {
        this.playerTwoScore++
      }
    }
  }
}
</script>
<style scoped>
  #game {
    width: 100%;
    height: 100%;
    background-color: black;
    position: relative;
    font-family: 'zig';
    border-top: 20px solid white;
    border-bottom: 20px solid white;
    overflow: hidden;
  }

  #centerLine {
    height: 100%;
    width: 18px;
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    background: repeating-linear-gradient(
      white,
      white 18px,
      black 18px,
      black 40px
    );
  }
</style>
