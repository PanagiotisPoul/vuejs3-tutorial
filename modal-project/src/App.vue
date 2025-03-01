<template>
  <h1>{{ title }}</h1>
  <p>Welcome...</p>

  <teleport to="#modals" v-if="showModal">
    <Modal :theme="theme" @close="toggleModal">
      <template v-slot:links>
        <a href="#">Enter contest</a>
        <a href="#">More info</a>
      </template>
      <h1>PoulPan</h1>
      <p>Hello friend!</p>
    </Modal>
  </teleport>

  <teleport to="#modals" v-if="loginRegister">
    <Modal @close="toggleLoginRegister">
      <template v-slot:login>
        <a href="#">Login</a>
        <a href="#">SignUp</a>
      </template>
      <h1>Login/Register</h1>
      <p>Not a user? Please register first!</p>
    </Modal>
  </teleport>

  <button @click.shift="toggleModal">open modal (shift)</button>
  <button @click="toggleLoginRegister">Login/Register</button>
</template>

<script>
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  components: { Modal },
  data() {
    return {
      title: "My First View App :)",
      // theme: "sale",
      theme: "test",
      showModal: false,
      loginRegister: false
    }
  },
    methods: {
      toggleModal() {
        this.showModal = !this.showModal;
      },
      toggleLoginRegister() {
        this.loginRegister = !this.loginRegister;
      }
    }
}
</script>

<style>
#app, #modals {
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
