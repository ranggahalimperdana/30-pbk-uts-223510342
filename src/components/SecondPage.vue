<template>
    <div>
      <h1>Halaman Kedua</h1>
      <button @click="$emit('navigate', 'HomePage')">Kembali ke Halaman Utama</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SecondPage'
  };
  </script>
  
  <style scoped>
  h1 {
    font-weight: 300;
  }
  
  button {
    margin-top: 1rem;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    cursor: pointer;
    background-color: #333;
    color: white;
    border: none;
    transition: background 0.3s;
  }
  
  button:hover {
    background-color: #555;
  }
  </style>
  