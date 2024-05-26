<template>
    <div class="flex items-center justify-center min-h-screen bg-gray-100">
      <div class="bg-white p-6 rounded shadow-md w-full max-w-md">
        <h2 class="text-2xl mb-4">Login</h2>
        <form @submit.prevent="login">
          <input v-model="email" type="email" placeholder="Email" class="w-full p-2 mb-4 border rounded" />
          <input v-model="password" type="password" placeholder="Password" class="w-full p-2 mb-4 border rounded" />
          <button type="submit" class="w-full bg-blue-500 text-white p-2 rounded">Login</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import api from '../services/api';
  
  export default {
    data() {
      return {
        email: '',
        password: '',
      };
    },
    methods: {
      async login() {
        try {
          const response = await api.post('/users/login', {
            email: this.email,
            password: this.password,
          });
          localStorage.setItem('token', response.data.token);
          this.$router.push('/');
        } catch (error) {
          console.error(error);
          alert(error.response.data.error);
        }
      },
    },
  };
  </script>
  