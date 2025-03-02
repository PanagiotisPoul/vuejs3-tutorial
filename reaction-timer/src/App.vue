<template>
  <div class="game-area">
    <div>
      <h1>Reaction Timer Project</h1>
      <button @click="start" :disabled="isPlaying || countdown > 0">{{ countdown > 0 ? countdown : 'Play' }}</button>
    </div>
    <div class="play-area">
      <TimerBlock v-if="isPlaying" :delay="delay" :randomX="randomX" :randomY="randomY" @end="endGame" />
      <GameResults v-if="!isPlaying" :score="score" />
    </div>
  </div>
</template>

<script>
import TimerBlock from './components/TimerBlock.vue'
import GameResults from './components/GameResults.vue'

export default {
  name: 'App',
  components: { TimerBlock, GameResults },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      randomX: 0,
      randomY: 0,
      countdown: 0
    }
  },
  methods: {
    start() {
      this.setRandomPosition();
      // this.delay = 2000 + Math.random() * 5000;  // 2s - 7s
      // console.log('random delay generated: ', this.delay)
      this.delay = 3000;
      let countdownInterval = setInterval(() => {
        this.countdown--;
        if (this.countdown === 0) {
          clearInterval(countdownInterval);
        }
      }, 1000);
      this.countdown = 3;
      this.isPlaying = true;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
    },
    setRandomPosition() {
      const playArea = document.querySelector('.play-area');
      const playAreaWidth = playArea.offsetWidth;
      const playAreaHeight = playArea.offsetHeight;
      console.log('offsetWidth', playAreaWidth)
      console.log('offsetHeight', playAreaHeight)
      this.randomX = Math.max(0, Math.random() * (playAreaWidth - 2) - 84);
      this.randomY = Math.max(0, Math.random() * (playAreaHeight - 2) - 104);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  display: flex;
  justify-content: center;
  justify-self: center;
}
.game-area {
  width: 100%;
}
.play-area {
  margin-top: 20px;
  width: 1000px;
  height: 1000px;
  border: 1px solid #000;
  position: relative;
  display: inline-block;
}
@media (min-width: 768px) and (max-width: 1023px) {
  .play-area {
    width: 700px;
    height: 800px
  }
}
@media (max-width: 425px) {
  .play-area {
    width: 90%;
    height: 600px
  }
}
button {
  width: 70px;
  height: 50px;
  border-radius: 10px;
  font-size: large;
  font-weight: 600;
  background-color: #efefef;
  cursor: pointer;
}
button[disabled] {
  cursor: not-allowed;
}
</style>
