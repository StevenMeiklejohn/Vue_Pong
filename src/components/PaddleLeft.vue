<template>
  <div id="paddle" :style="{
                        left: xPos + 'px',
                        top: yPos + 'px',
                    }"></div>
</template>

<script>
import { eventBus } from '@/main'
export default {
  name: 'PaddleLeft',
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
    this.xPos = this.isLeftPaddle ? 15 : this.$parent.$refs.game.clientWidth - 35
    eventBus.$emit('PaddleLeftPosition', {xPos: this.xPos, ypos: this.yPos})
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
      eventBus.$emit('PaddleLeftPosition', {xPos: this.xPos, yPos: this.yPos})
    }
  }
}
</script>

<style scoped>
    #paddle {
        width: 20px;
        height: 100px;
        background-color: white;
        position: absolute;
        left: 10px;
        top: 500px;
    }
</style>
