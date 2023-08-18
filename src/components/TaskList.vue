<script setup lang="ts">
import { ref } from 'vue'
import { computed } from 'vue'
interface Task {
  name: string
  situation: number
}

const tasks = ref<Task[]>([])
// 完了済みタスクを計算して保持しておく
const finishedTasks = computed(() => tasks.value.filter((task) => task.situation === 1))
// 未完タスクを計算して保持しておく
const notFinishedTasks = computed(() => tasks.value.filter((task) => task.situation === 0))
const newTaskName = ref('')

const addTask = () => {
  if (newTaskName.value !== '') tasks.value.push({ name: newTaskName.value, situation: 0 })
  newTaskName.value = ''
}
</script>

<template>
  <div>未完了タスク</div>
  <ul>
    <li v-for="task in notFinishedTasks" :key="task.name">
      <div>タスク名:{{ task.name }}</div>
      <button @click="task.situation++">完了にする</button>
    </li>
  </ul>
  <div>完了済タスク</div>
  <ul>
    <li v-for="task in finishedTasks" :key="task.name">
      <div>タスク名:{{ task.name }}</div>
      <button @click="task.situation--">未完了にする</button>
    </li>
  </ul>
  <label>
    タスク名
    <input v-model="newTaskName" type="text" />
  </label>

  <button @click="addTask">追加</button>
</template>
