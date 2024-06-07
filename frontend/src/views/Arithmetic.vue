<template>
    <div class="arithmetic-container">
      <h2>Arithmetic Operations</h2>
      <form @submit.prevent="performOperation" class="operation-form">
        <div class="form-group">
          <label for="num1">Number 1:</label>
          <input type="number" v-model="num1" required class="form-control" />
        </div>
        <div class="form-group">
          <label for="num2">Number 2:</label>
          <input type="number" v-model="num2" required class="form-control" />
        </div>
        <div class="form-group">
          <label for="operation">Operation:</label>
          <select v-model="operation" class="form-control">
            <option value="add">Add</option>
            <option value="subtract">Subtract</option>
            <option value="multiply">Multiply</option>
            <option value="divide">Divide</option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary">Calculate</button>
      </form>
      <p v-if="result !== null" class="result-message">Result: {{ result }}</p>
      <p v-if="error" class="error-message">{{ error }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        num1: null,
        num2: null,
        operation: 'add',
        result: null,
        error: null,
      };
    },
    methods: {
      async performOperation() {
        this.error = null;
        try {
          const token = localStorage.getItem('token');
          const response = await axios.post(`http://localhost:7000/${this.operation}`, {
            num1: this.num1,
            num2: this.num2,
          }, {
            headers: {
              'Authorization': `Bearer ${token}`,
            },
          });
          this.result = response.data.result;
        } catch (err) {
          this.error = err.response ? err.response.data.message : 'An error occurred. Please try again later.';
          this.result = null;
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .arithmetic-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
  }
  
  .operation-form {
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 10px;
  }
  
  .result-message {
    color: #5cb85c;
    margin-top: 10px;
  }
  
  .error-message {
    color: #d9534f;
    margin-top: 10px;
  }
  </style>
  