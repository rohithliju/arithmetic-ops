<template>
    <div id="app" class="app-container">
      <router-view></router-view>
    </div>
  </template>
  
  <script>
  export default {
    name: 'App',
  };
  </script>
  
  <style>
  /* Global styles */
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
  }
  
  .app-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }
  </style>
  