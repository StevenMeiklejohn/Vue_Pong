<template>
  <div id="paddle" :style="{
                        left: xPos + 'px',
                        top: yPos + 'px',
                    }"></div>
</template>

<script>
import { eventBus } from '@/main'
export default {
  name: 'PaddleRight',
  props: {
    isLeftPaddle: {
      type: Boolean
    }
  },
  data () {
    return {
      xPos: 0,
      yPos: 0
    }
  },
  mounted () {
    this.yPos = this.$parent.$refs.game.clientHeight / 2 - 50
    this.xPos = this.$parent.$refs.game.clientWidth - 25
    eventBus.$emit('PaddleRightPosition', {xPos: this.xPos, ypos: this.yPos})
  },
  created: function () {
    window.addEventListener('keydown', this.keyPressed)
  },
  methods: {
    keyPressed (e) {
      if (this.isLeftPaddle && e.key === 'w' && this.yPos > 0) {
        this.yPos = this.yPos - 30
      }
      if (this.isLeftPaddle && e.key === 's' && this.yPos < this.$parent.$refs.game.clientHeight - 100) {
        this.yPos = this.yPos + 30
      }
      if (!this.isLeftPaddle && e.key === 'ArrowUp' && this.yPos > 0) {
        this.yPos = this.yPos - 30
      }
      if (!this.isLeftPaddle && e.key === 'ArrowDown' && this.yPos < this.$parent.$refs.game.clientHeight - 100) {
        this.yPos = this.yPos + 30
      }
      eventBus.$emit('PaddleRightPosition', {xPos: this.xPos, yPos: this.yPos})
    }
  }
}
</script>

<style scoped>
    #paddle {
      width: 20px;
      height: 100px;
      border: 1px solid orange; /* some kind of blue border */
      /* other CSS styles */

      /* round the corners */
    /* -webkit-border-radius: 100%;
       -moz-border-radius: 100%;
            border-radius: 100%; */

    /* make it glow! */
    -webkit-box-shadow: 0px 0px 15px #f5af1a;
       -moz-box-shadow: 0px 0px 15px #f5af1a;
            box-shadow: 0px 0px 15px #f5af1a; /* some variation of blue for the shadow */
    background:orange;



        /* width: 20px;
        height: 100px;
        background-color: white; */
        position: absolute;
        left: 10px;
        top: 500px;
    }
</style>
