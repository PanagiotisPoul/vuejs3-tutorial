<template>
  <div>
    <form @submit.prevent="submitForm">
      <label>Email:</label>
      <input
        type="email"
        placeholder="Type your email"
        required
        v-model="email"
      >

      <label>Password:</label>
      <input
        type="password"
        placeholder="Type your password"
        required
        v-model="password"
      >
      <div v-if="pswError" class="error"> {{ pswErrMsg }}</div>

      <label>Role:</label>
      <select
        v-model="role"
      >
        <option disabled value="">Select a role</option>
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <label>Skills:</label>
      <input
        type="text"
        placeholder="Type in your skills and press comma after each entry"
        v-model="tempSkill"
        @keyup="addSkill"
      >
      <div
        v-for="(skill, index) in skills"
        :key="index"
        class="pill"
        @click="removeSkill(index)"
      >
        {{ skill }}
      </div>

      <div class="terms">
        <input
          type="checkbox"
          required
          v-model="terms"
        >
        <label>Accept terms and conditions</label>
      </div>

      <!-- <div class="names">
        <input
          type="checkbox"
          value="shaun"
          v-model="names"
        >
        <label>Shaun</label>
        <input
          type="checkbox"
          value="yoshi"
          v-model="names"
        >
        <label>Yoshi</label>
        <input
          type="checkbox"
          value="mario"
          v-model="names"
        >
        <label>Mario</label>
      </div> -->

      <div class="submit">
        <button>Create an Account</button>
      </div>
    </form>

    <!-- <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms accepted: {{ terms }}</p> -->
    <!-- <p>Names: {{ names }}</p> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      // names: [],
      tempSkill: '',
      skills: [],
      pswError: false,
      pswErrMsg: 'Password must be at least 6 characters long',
    }
  },
  methods: {
    addSkill(e) {
      if ( (e.key === ',' || e.keyCode === 188 || e.code === 'Comma') ) {
        const skill = this.tempSkill.toUpperCase().replace(/[\[\]{};:'",<.>\/?§±`~\-_=\+!@#$%^&*()\\|]/g, '');
        if (!this.skills.includes(skill)) {
          this.skills.push(skill);
        }
        this.tempSkill = '';
      } else {
        this.tempSkill = e.target.value;
        console.log('e', e)
      }
    },
    removeSkill(index) {
      this.skills.splice(index, 1);
    },
    submitForm() {
      // validate password
      this.pswError = this.password.length > 5 ? false : true;
      if (!this.pswError) {
        console.log('submitted')
        console.log('Email:', this.email)
        console.log('Password:', this.password)
        console.log('Role:', this.role)
        console.log('skills', this.skills)
        console.log('Terms accepted:', this.terms)
      }
    }
  }
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input, select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.names label {
  margin-right: 10px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>