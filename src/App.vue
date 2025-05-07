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

