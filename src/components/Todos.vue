<template>
    <div class="background">
      <h1>{{ pageTitle }}</h1>
  
      <p>{{ tableTitle }}</p> <br>
      <!-- Displaying activities in a table -->
      <table>
        <thead>
          <tr>
            <th>Kegiatan</th>
            <th>Status</th>
            <th>Tindakan</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="activity in activities" :key="activity.id" :class="{ completed: activity.completed }">
            <td>
              <!-- If activity is completed, display with strikethrough -->
              <span :style="{ 'text-decoration': activity.completed ? 'line-through' : 'none' }">{{ activity.name }}</span>
            </td>
            <td>
              <!-- If activity is completed, display 'Telah Selesai', otherwise 'Belum Selesai' -->
              <span>{{ activity.completed ? 'Telah Selesai' : 'Belum Selesai' }}</span>
              <input type="checkbox" v-model="activity.completed">
            </td>
            <td>
              <button @click="cancelActivity(activity.id)">Hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <!-- Form to add a new activity -->
      <form @submit.prevent="addActivity"> <br>
        <input type="text" v-model="newActivity" placeholder="Tambahkan Kegiatan"> <br>
        <button type="submit">Tambahkan</button>
      </form>
    </div>
  
    <!-- Footer -->
    <footer>
      <p>&copy; 2024 Nurul Hayana Putri</p>
    </footer>
  </template>
  
  <script>
  export default {
    data() {
      return {
        pageTitle: "Nurul Hayana Putri - 223510821",
        tableTitle: "Tabel Kegiatan",
        author: "Nurul Hayana Putri",
        activities: [
          { id: 1, name: 'Memasak', completed: false },
          { id: 2, name: 'Shopping', completed: false },
          { id: 3, name: 'Membaca Buku', completed: false },
          { id: 4, name: 'Menari', completed: false }
        ],
        newActivity: ''
      };
    },
    methods: {
      addActivity() {
        if (this.newActivity.trim() !== '') {
          this.activities.push({ id: Date.now(), name: this.newActivity, completed: false });
          this.newActivity = '';
        }
      },
      cancelActivity(id) {
        const index = this.activities.findIndex(activity => activity.id === id);
        if (index !== -1) {
          this.activities.splice(index, 1);
        }
      }
    }
  };
  </script>
  
  <style>
  body {
    margin: 0;
    padding: 0;
  }
  /* CSS for the main container */
  .background {
    background-image: url(image/1.jpg);
    color: white;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    min-height: 100vh;
    padding: 20px;
  }
  /* Styling for completed activities */
  .completed {
    filter: blur(0.5px);
  }
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    border: 1px solid white;
    padding: 8px;
    text-align: left;
  }
  /* Adding strikethrough for completed activities */
  .completed span {
    text-decoration: line-through;
  }
  /* CSS for footer */
  footer {
    background-color: grey;
    color: white;
    text-align: center;
    padding: 5px 0;
    position: fixed;
    bottom: 0;
    width: 100%;
  }
  /* CSS for input */
  input[type="text"] {
    width: 200px;
    padding: 8px;
    margin-bottom: 10px;
  }
  /* CSS for submit button */
  button[type="submit"] {
    background-color: white;
    color: black;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
  }
  </style>
  