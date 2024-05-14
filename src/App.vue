<!-- App.vue -->
<template>
  <div>
    <nav>
      <ul>
        <li @click="selectedMenu = 'todos'">Todos</li>
        <li @click="selectedMenu = 'posts'">Posts</li>
      </ul>
    </nav>
    <div>
      <Todos v-if="selectedMenu === 'todos'" />
      <users v-if="selectedMenu === 'posts'" />
    </div>
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import users from './components/users.vue';

export default {
  components: {
    Todos,
    users,
  },
  data() {
    return {
      selectedMenu: '', 
    };
  },
};
</script>

<style scoped>
 .background {
    background-image: url(image/1.jpg);
    color: white;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    min-height: 100vh;
    padding: 20px;
  }
nav {
  background-color: grey;
  padding: 15px;
  color: white;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
</style>
