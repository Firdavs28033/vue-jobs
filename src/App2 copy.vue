<script>
  export default {
    data() {
      return {
        name: '',
        status: 'pending',
        tasks: ['Task 1', 'Task 2', 'Task 3'],
        link: 'google.com',
        isVisible: false,
        message: 'Assalomu alaykum hammaga'
      };
    },
    methods: {
      sayHello() {
        alert("Hello");
      },
      toggleStatus() {
        if (this.status === 'active') {
          this.status = 'pending';
        } else if (this.status === 'pending') {
          this.status = 'inactive'
        } else {
          this.status = 'active'
        }
      }
    },
  };
</script>

<template>
  <h1>Hello World!</h1> <br>
  <p>{{ name }}</p> <br>
  <p v-if="status === 'uchar'">Assalomu alaykum</p>
  <p v-else-if="status === 'pending'">Pendingjon</p>
  <p v-else>Xayr sog' bo'ling</p>

  <h1>Tasks</h1>
  <!-- <p v-for="task in tasks" :key="task">{{ task }}</p> -->
  <p v-for="(task, index) in tasks" :key="task">{{ index + 1 }} - {{ task }}.</p>
  <button><a :href="link">Tap to Google</a></button> <br>
  <!-- <button><a v-bind:href="link">Tap to Google</a></button> -->
   <input type="text" placeholder="Name" v-model="name">
   <p>Salom, {{ name }}</p>
   <p v-show="isVisible">Matn</p>
   <button @click="sayHello">Salom</button>
   <p v-text="message"></p>
   <button v-on:click="toggleStatus">Change</button>
</template>
