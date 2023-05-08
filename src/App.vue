<template>
  <div>
    <h1>Tasks List</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <strong>{{ task.title }}</strong>
        <p>{{ task.description }}</p>
      </li>
    </ul>
  </div>
  <chatbot/>
</template>

<script>
import axios from 'axios';
import chatbot from './components/chatbot'

export default {
  name: 'App',
  components: {
    chatbot,
  },
  data() {
    return {
      tasks: []
    };
  },
  created() {
    this.fetchTasks();
  },
  methods: {
    fetchTasks() {
      axios.get('http://localhost:8000/tasks')
        .then(response => {
          this.tasks = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
};
</script>
