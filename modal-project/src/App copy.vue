<template>
  <h1>{{ title }}</h1>
  <div>
    <input type="text" ref="boo">
    <button @click="handleClick">click me</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      title: "My First View App :)"
    }
  },
  methods: {
    handleClick() {
      console.log('test:', this.$refs.boo)
      this.$refs.boo.classList.add('active')
      this.$refs.boo.focus()
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
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
</style>
