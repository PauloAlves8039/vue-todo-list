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
    },
    async completeTask(id) {
      await axios.put(`${baseURL}/${id}`, { done: true });
      this.todos = this.todos.map((todo) => {
        if (todo.id === id) {
          todo.done = true;
        }
        return todo;
      });
    },
    removeTask(id) {
      axios.delete(`${baseURL}/${id}`);
      this.todos = this.todos.filter((todo) => todo.id !== id);
    }

  }
}
</script>

<style scoped>

</style>
