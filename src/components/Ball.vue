/* eslint-disable */
<template>
  <div id="ball" :style="{
                            width: size + 'px',
                            height: size + 'px',
                            left: xPos + 'px',
                            top: yPos + 'px',
                          }"></div>
</template>

<script>
import { eventBus } from '@/main'
export default {
  name: 'Ball',
  data () {
    return {
      size: 20,
      xPos: 0,
      yPos: 0,
      xDir: '',
      yDir: '',
      speed: 0,
      interval: null,
      leftPaddlePosition: null,
      rightPaddlePosition: null
    }
  },
  methods: {
    move () {
      if (this.xDir === 'leftToRight') {
        this.xPos = this.xPos + this.speed
      } else {
        this.xPos = this.xPos - this.speed
      }
      if (this.yDir === 'bottomToTop') {
        this.yPos = this.yPos + this.speed
      } else {
        this.yPos = this.yPos - this.speed
      }
      this.checkForWall()
      this.checkPaddleHit()
      this.checkIfScored()
    },
    reverseDirection (hitLeftPaddle, hitTopHalfOfPaddle) {
      if (hitLeftPaddle) {
        this.xDir = 'leftToRight'
      } else {
        this.xDir = 'rightToLeft'
      }
      if (hitTopHalfOfPaddle) {
        this.yDir = 'bottomToTop'
      } else {
        this.yDir = 'topToBottom'
      }
    },
    reset () {
      this.yPos = (this.$parent.$refs.game.clientHeight - this.size) / 2
      this.xPos = (this.$parent.$refs.game.clientWidth - this.size) / 2
    },
    accelerate (force) {
      this.speed = this.speed + force
    },
    startMoving () {
      const randomNumber1 = Math.random()
      const randomNumber2 = Math.random()
      this.speed = 10
      randomNumber1 < 0.5 ? this.xDir = 'leftToRight' : this.xDir = 'rightToLeft'
      randomNumber2 < 0.5 ? this.yDir = 'bottomToTop' : this.yDir = 'topToBottom'
      this.interval = setInterval(this.move, 100)
    },
    checkForWall () {
      if (this.yPos > this.$parent.$refs.game.clientHeight - this.size) {
        this.yDir = 'topToBottom'
      }
      if (this.yPos < this.size) {
        this.yDir = 'bottomToTop'
      }
    },
    checkPaddleHit () {
      if ((this.xPos < this.leftPaddlePosition.xPos + 20) && (this.yPos < this.leftPaddlePosition.yPos + 100) && (this.yPos > this.leftPaddlePosition.yPos - 100)) {
        this.xDir = 'leftToRight'
      }
      if ((this.xPos > this.rightPaddlePosition.xPos - 20) && (this.yPos < this.rightPaddlePosition.yPos + 100) && (this.yPos > this.rightPaddlePosition.yPos - 100)) {
        console.log('redirect');
        this.xDir = 'rightToLeft'
      }
    },
    checkIfScored () {
      if (this.xPos > this.$parent.$refs.game.clientWidth - (this.size * 1.5)) {
        this.$emit('goal', 'playerOne')
        this.countScoreAndReset()
      }
      if (this.xPos < this.size / 2) {
        this.$emit('goal', 'playerTwo')
        this.countScoreAndReset()
      }
    },
    countScoreAndReset () {
      clearInterval(this.interval)
      setTimeout(() => {
        this.reset()
        this.startMoving()
      }, 3000)
    }
  },
  mounted () {
    eventBus.$on('PaddleLeftPosition', (position) => {
      this.leftPaddlePosition = position
    })
    eventBus.$on('PaddleRightPosition', (position) => {
      this.rightPaddlePosition = position
    })
    this.reset()
    this.startMoving()
  }
}
</script>

<style scoped>
  #ball {
    border: 1px solid orange; /* some kind of blue border */
    /* other CSS styles */

    /* round the corners */
    -webkit-border-radius: 100%;
       -moz-border-radius: 100%;
            border-radius: 100%;

    /* make it glow! */
    -webkit-box-shadow: 0px 0px 15px #f5af1a;
       -moz-box-shadow: 0px 0px 15px #f5af1a;
            box-shadow: 0px 0px 15px #f5af1a; /* some variation of blue for the shadow */
    background:orange;

    /* background: white; */
    position: absolute;
    /* border-radius: 100%; */
    /* transition: all linear; */
  }
</style>
