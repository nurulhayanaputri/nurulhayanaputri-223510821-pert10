<template>
    <div class="background">
      <div class="container">
        <h1>Users</h1>
        <select v-model="selectedUser" class="select">
          <option v-for="user in users" :key="user.id" :value="user.id">
            {{ user.name }}
          </option>
        </select>
        <div v-if="isLoading" class="loading">Loading posts...</div>
        <div v-else class="posts-container">
          <h2>Posts</h2>
          <ul class="posts-list">
            <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
          </ul>
        </div>
      </div>
    </div>
        <!-- Footer -->
        <footer>
        <p>&copy; 2024 Nurul Hayana Putri</p>
      </footer>
  </template>
  
  <script setup>
  import { ref, watch } from "vue";
  
  const users = ref([]);
  const posts = ref([]);
  const selectedUser = ref(null);
  const isLoading = ref(false);
  
  const getUsers = async () => {
    const resource = "https://jsonplaceholder.typicode.com/users";
    const response = await fetch(resource);
    users.value = await response.json();
  };
  
  const getPosts = async () => {
    if (selectedUser.value !== null) {
      posts.value = [];
      isLoading.value = true;
      const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
      posts.value = await response.json();
      isLoading.value = false;
    }
  };
  
  getUsers();
  
  watch(selectedUser, getPosts);
  </script>
  
  <style scoped>
  .background {
    background-image: url('image/1.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    min-height: 100vh;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .container {
    text-align: center;
  }
  
  .select {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
  }
  
  .loading {
    color: white;
  }
  
  .posts-container {
    color: white;
  }
  
  .posts-list {
    padding: 0;
  }
  
  li {
    list-style-type: none;
    margin-bottom: 10px;
  }
  </style>
  