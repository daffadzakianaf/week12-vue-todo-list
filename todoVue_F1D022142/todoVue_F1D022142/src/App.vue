<script setup>
import { ref } from 'vue';

// State
const tasks = ref([]);
const newTask = ref("");

// Tambah tugas
function addTask() {
  if (newTask.value.trim() === "") {
    alert("Tugas tidak boleh kosong!");
    return;
  }
  tasks.value.push(newTask.value);
  newTask.value = "";
}

// Hapus tugas
function deleteTask(index) {
  tasks.value.splice(index, 1);
}
</script>

<template>
  <div class="container">
    <h1>To-Do List Vue.js</h1>

    <!-- Form input -->
    <form @submit.prevent="addTask">
      <input 
        v-model="newTask" 
        type="text" 
        placeholder="Masukkan tugas baru..."
      />
      <button type="submit">Tambah</button>
    </form>

    <!-- Jika kosong -->
    <p v-if="tasks.length === 0" class="empty">Tidak ada tugas</p>

    <!-- Tampilkan list tugas -->
    <ul v-else>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task }}
        <button class="delete" @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style>
.container {
  width: 350px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
  text-align: center;
}

input {
  width: 70%;
  padding: 8px;
  margin-right: 5px;
}

button {
  padding: 8px 12px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 15px;
}

li {
  padding: 8px;
  background: #f0f0f0;
  margin-bottom: 8px;
  display: flex;
  justify-content: space-between;
}

.delete {
  background: red;
  color: white;
  border: none;
  padding: 4px 8px;
}

.empty {
  color: gray;
  margin-top: 15px;
}
</style>

