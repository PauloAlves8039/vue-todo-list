<template>
  <div>
    
  </div>
</template>

<script>
import axios from "axios";
const baseURL = "http://localhost:3001/todos";

export default {
  name: 'TodoList',
  data () {
    return {
      todos: [],
      todoName: "",
    }
  },
  async created() {
    try {
      const getTasks = await axios.get(baseURL);
      this.todos = getTasks.data;
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    async addTask() {
      const postTask = await axios.post(baseURL, { name: this.todoName});
      this.todos = [...this.todos, postTask.data];
    }
  }
}
</script>

<style scoped>

</style>
