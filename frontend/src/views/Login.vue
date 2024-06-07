<template>
    <div class="login-container">
      <h2>Login</h2>
      <form @submit.prevent="login" class="login-form">
        <div class="form-group">
          <label for="username">Username:</label>
          <input type="text" v-model="username" required class="form-control" />
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input type="password" v-model="password" required class="form-control" />
        </div>
        <button type="submit" class="btn btn-primary">Login</button>
      </form>
      <p v-if="error" class="error-message">{{ error }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        username: '',
        password: '',
        error: null,
      };
    },
    methods: {
      async login() {
        this.error = null;
        try {
          const response = await axios.post('http://localhost:7000/login', {
            username: this.username,
            password: this.password,
          });
          localStorage.setItem('token', response.data.token);
          this.$router.push('/arithmetic');
        } catch (err) {
          if (err.response && err.response.status === 401) {
            this.error = 'Invalid username or password';
          } else {
            this.error = 'An error occurred. Please try again later.';
          }
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
  }
  
  .login-form {
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 10px;
  }
  
  .error-message {
    color: #d9534f;
    margin-top: 10px;
  }
  </style>
  