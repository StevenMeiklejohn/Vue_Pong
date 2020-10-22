<template>
  <div id="scoreboard">
    <div class="playerScore" id="playerOneScore">{{playerOneScore}}</div>
    <div class="playerScore" id="playerTwoScore">{{playerTwoScore}}</div>
  </div>
</template>

<script>
export default {
  name: 'Scoreboard',
  props: {
    playerOneScore: {
      type: Number,
      required: true
    },
    playerTwoScore: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      leader: null
    }
  }
}
</script>

<style scoped>
  #scoreboard {
    position: absolute;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    width: 300px;
    height: 150px;
  }

  .playerScore {
    color: orange;
    /* -webkit-box-shadow: 0px 0px 15px #f5af1a; */
       /* -moz-box-shadow: 0px 0px 15px #f5af1a;
            box-shadow: 0px 0px 15px #f5af1a; */
    font-size: 5em;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    font-family: 'impact';
  }

  #playerOneScore {
    left: 0px;
  }

  #playerTwoScore {
    right: 0px;
  }
</style>
