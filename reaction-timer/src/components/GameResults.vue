<template>
  <div class="results" v-if="this.score">
    <p>Reaction Time: <span>{{ score }}</span>ms</p>
    <p :style="rankColor">{{ rank }}</p>
  </div>
</template>

<script>
export default {
  props: ['score'],
  data() {
    return {
      rank: null,
      color: null
    }
  },
  mounted() {
    if (this.score <= 550) {
      this.rank = 'Ninja Fingers';
      this.color = 'green';
    } else if ( this.score <= 700) {
      this.rank = 'Rapid Reflexes';
      this.color = 'orange';
    } else {
      this.rank = 'Snail pace...';
      this.color = 'red';
    }
  },
  computed: {
    rankColor() {
      return {
        margin: 0,
        color: `${this.color}`
      };
    }
  },
}
</script>

<style>
.results {
  font-size: large;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.results p {
  border: 1px solid #444;
  width: 250px;
  padding: 20px 0;
  margin-top: 50px;
  border-radius: 20px;
  color: #444;
  font-weight: 500;
  background-color: #efefef;
}
.results span {
  color: blue;
  font-weight: 600;
  font-size: larger;
}
</style>
