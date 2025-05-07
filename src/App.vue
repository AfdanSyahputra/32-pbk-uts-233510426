<template>
  <div class="app-container">
    <h1>DAFTAR KEGIATAN</h1>

    <div class="form-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambah Aktivitas baru..." />
      <button @click="addTask">Tambah</button>
    </div>

    <div class="filter-group">
      <label>
        <input type="checkbox" v-model="showIncompleteOnly" />
        Tampilkan kegiatan yang belum selesai
      </label>
    </div>

    <ul class="task-list">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="{ done: task.done }"
      >
        <input type="checkbox" v-model="task.done" />
        <span>{{ task.text }}</span>
        <button @click="removeTask(index)">Batal</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const tasks = ref([])
const showIncompleteOnly = ref(false)

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, done: false })
    newTask.value = ''
  }
}

function removeTask(index) {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() => {
  return showIncompleteOnly.value
    ? tasks.value.filter(task => !task.done)
    : tasks.value
})

</script>
<style scoped>
.app-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 30px;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
  font-family: 'Inter', sans-serif;
  color: #333;
  transition: background 0.3s, color 0.3s;
}

h1 {
  text-align: center;
  margin-bottom: 24px;
  font-size: 28px;
  color: #2c3e50;
}

.form-group {
  display: flex;
  gap: 12px;
  margin-bottom: 24px;
}

input[type="text"] {
  flex: 1;
  padding: 10px 14px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.3s;
}

input[type="text"]:focus {
  outline: none;
  border-color: #42b983;
}

button {
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  background-color: #303ca5;
  color: white;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #369e6f;
}

.filter-group {
  margin-bottom: 16px;
  font-size: 14px;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f7f9fa;
  padding: 12px 16px;
  border-radius: 10px;
  border-left: 4px solid #42b983;
  margin-bottom: 10px;
  transition: background 0.3s;
}

.task-list li:hover {
  background: #eef3f5;
}

.task-list li.done span {
  text-decoration: line-through;
  color: #999;
}

.task-list input[type="checkbox"] {
  margin-right: 10px;
  transform: scale(1.2);
}

.task-list span {
  flex: 1;
  font-size: 15px;
}

.task-list button {
  background-color: #e74c3c;
  padding: 6px 12px;
  font-size: 13px;
}

.task-list button:hover {
  background-color: #c0392b;
}

/* Dark Mode Support */
@media (prefers-color-scheme: dark) {
  .app-container {
    background: #1e1e1e;
    color: #ddd;
    box-shadow: 0 10px 25px rgba(255, 255, 255, 0.05);
  }

  input[type="text"] {
    background: #2b2b2b;
    color: #eee;
    border: 1px solid #555;
  }

  input[type="text"]::placeholder {
    color: #888;
  }

  .task-list li {
    background: #2a2a2a;
    border-left-color: #42b983;
  }

  .task-list li:hover {
    background: #333;
  }

  .task-list li.done span {
    color: #777;
  }

  .filter-group {
    color: #ccc;
  }
}
</style>


