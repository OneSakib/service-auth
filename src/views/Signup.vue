<template>
  <div class="container my-5">
    <h5 class="text-center">Signup</h5>
    <form @submit.prevent="signup">
      <div class="row">
        <div class="offset-3 col-6">
          <div class="mb-3">
            <label for="name" class="form-label">Name</label>
            <input type="text" class="form-control" id="name" placeholder="Name" v-model="formData.name">
          </div>
          <div class="mb-3">
            <label for="email" class="form-label">Email address</label>
            <input type="email" class="form-control" id="email" placeholder="name@example.com" v-model="formData.email">
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input type="password" class="form-control" id="password" placeholder="password"
              v-model="formData.password">
          </div>
          <button type="submit" class="btn btn-secondary">Signup</button>
          <RouterLink class="d-block mt-4" to="/login">Login</RouterLink>
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
    async signup() {
      try {
        const response = await axios.post('https://sakibapi.onrender.com/api/auth/register', {
          name: this.formData.name,
          email: this.formData.email,
          password: this.formData.password
        });

        // Assuming the token is in response.data.token
        localStorage.setItem('authToken', response.data.token);
        localStorage.setItem('userName', response.data.name);
        this.$router.push({ name: 'home' });
      } catch (err) {
        this.error = 'Signup failed. Please try again.';
      }
    }
  }
};
</script>

<style>
/* Add styles here if needed */
</style>
