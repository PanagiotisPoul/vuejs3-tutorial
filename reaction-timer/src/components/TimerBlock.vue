<template>
  <div class="block">
    <p :style="positionStyle" v-if="showBlock" @click="stopTimer">Click me</p>
  </div>
</template>

<script>
export default {
  props: ['delay', 'randomX', 'randomY'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
      left: this.randomX,
      top: this.randomY
    }
  },
  mounted() {
    console.log('left', this.left)
    console.log('top', this.top)
    console.log('timeout started at mounted')
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay)
  },
  updated() {
    console.log('component updated after: ', this.delay)
  },
  computed: {
    positionStyle() {
      return {
        position: 'absolute',
        left: `${this.left}px`,
        top: `${this.top}px`
      };
    }
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      console.log('score', this.reactionTime)
      this.$emit('end', this.reactionTime)
    }
  }
}
</script>

<style>
.block p {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: large;
  cursor: pointer;
  border: 2px solid #000;
  width: 80px;
  height: 60px;
  padding: 20px 0;
  margin-top: 0;
  border-radius: 50%;
  color: #fff;
  font-weight: 900;
  background-color: #0faf87;
  letter-spacing: 0.5px;
}
</style>