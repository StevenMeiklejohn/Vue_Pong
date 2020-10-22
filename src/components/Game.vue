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
    border: 20px solid orange; /* some kind of blue border */
    /* other CSS styles */

    /* round the corners */
    /* -webkit-border-radius: 100%;
       -moz-border-radius: 100%;
            border-radius: 100%; */

    /* make it glow! */
    -webkit-box-shadow: 0px 0px 15px #f5af1a;
       -moz-box-shadow: 0px 0px 15px #f5af1a;
            box-shadow: 0px 0px 15px #f5af1a; /* some variation of blue for the shadow */
    /* background:orange;
    width: 100%;
    height: 100%;
    background-color: black;
    position: relative;
    font-family: 'zig';
    border-top: 20px solid white;
    border-bottom: 20px solid white;
    overflow: hidden; */
  }

  #centerLine {
    height: 92%;
    width: 18px;
    position: absolute;
    top: 16px;
    left: 50%;
    transform: translateX(-50%);
    -webkit-box-shadow: 0px 0px 15px #f5af1a;
      -moz-box-shadow: 0px 0px 15px #f5af1a;
           box-shadow: 0px 0px 15px #f5af1a; /* some variation of blue for the shadow */
    background: repeating-linear-gradient(
      #f5af1a,
      #f5af1a 18px,
      black 18px,
      black 40px
    );
  }
</style>
