<template>
    <div class="flex items-center justify-center min-h-screen bg-gray-100">
      <div class="bg-white p-6 rounded shadow-md w-full max-w-md">
        <h2 class="text-2xl mb-4">Register</h2>
        <form @submit.prevent="register">
          <input v-model="username" type="text" placeholder="Username" class="w-full p-2 mb-4 border rounded" />
          <input v-model="email" type="email" placeholder="Email" class="w-full p-2 mb-4 border rounded" />
          <input v-model="password" type="password" placeholder="Password" class="w-full p-2 mb-4 border rounded" />
          <button type="submit" class="w-full bg-blue-500 text-white p-2 rounded">Register</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import api from '../services/api';
  
  export default {
    data() {
      return {
        username: '',
        email: '',
        password: '',
      };
    },
    methods: {
      async register() {
        try {
          const response = await api.post('/users/register', {
            username: this.username,
            email: this.email,
            password: this.password,
          });
          alert(response.data.message);
          this.$router.push('/login');
        } catch (error) {
          console.error(error);
          alert(error.response.data.error);
        }
      },
    },
  };
  </script>
  