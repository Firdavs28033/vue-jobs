<script setup>
import { ref, onMounted } from 'vue';

const name = ref('');
const status = ref('pending');
const tasks = ref([]);
const link = ref('https://google.com');
const isVisible = ref(false);
const message = ref('Assalomu alaykum everyone');
const newTask = ref('');  // Yangi vazifa uchun ref

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
};

const sayHello = () => {
  alert('Hello');
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';  // Yangi vazifa qo'shilgandan keyin inputni bo'shatish
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);  // Taskni index orqali o'chirish
};

onMounted(async () => {
  try {
    const response = await fetch('https://dummyjson.com/todos');
    const data = await response.json(); // await bilan kutib olish
    // API javobining todos maydonidan vazifalarni olish
    tasks.value = data.todos.map((task) => task.todo); // "todo" qiymatini olish
  } catch (error) {
    console.log('Error fetching tasks:', error);
  }
});
</script>

<template>
  <h1>Hello World!</h1> <br>
  <p>{{ name }}</p> <br>
  <p v-if="status === 'active'">Assalomu alaykum</p>
  <p v-else-if="status === 'pending'">Pendingjon</p>
  <p v-else>Xayr sog' bo'ling</p>

  <button><a :href="link">Tap to Google</a></button> <br>

  <input type="text" placeholder="Name" v-model="name">
  <p>Salom, {{ name }}</p>
  <p v-show="isVisible">Matn</p>
  <button @click="sayHello">Salom</button>
  <p v-text="message"></p>

  <button v-on:click="toggleStatus">Change</button><br><br>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>
  <h1>Tasks</h1>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ index + 1 }}. {{ task }}</span>
      <button @click="deleteTask(index)">X</button> <!-- index ni uzatish kerak -->
    </li>
  </ul>
</template>
