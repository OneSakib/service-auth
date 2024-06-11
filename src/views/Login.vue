<template>
  <div class="container my-5">
    <h5 class="text-center">Login</h5>
    <form @submit.prevent="login">
      <div class="row">
        <div class="offset-3 col-6">
          <div class="mb-3">
            <label for="email" class="form-label">Email address</label>
            <input type="email" class="form-control" id="email" placeholder="name@example.com" v-model="formData.email">
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input type="password" class="form-control" id="password" placeholder="password"
              v-model="formData.password">
          </div>
          <button type="submit" class="btn btn-secondary">Login</button>
          <RouterLink class="d-block mt-4" to="/signup">Signup</RouterLink>
          <p v-if="error">{{ error }}</p>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        password: ''
      },
      error: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post(' https://sakibapi.onrender.com/api/auth/login', {
          email: this.formData.email,
          password: this.formData.password
        });

        // Assuming the token is in response.data.token
        localStorage.setItem('authToken', response.data.token);
        localStorage.setItem('userName', response.data.name);
        this.$router.push({ name: 'home' });
      } catch (err) {
        this.error = 'Invalid credentials or network error';
      }
    }
  }
};
</script>

<style>
/* Add styles here if needed */
</style>
