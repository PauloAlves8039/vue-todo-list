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
    }
  },
  async created() {
    try {
      const response = await axios.get(baseURL);
      this.todos = response.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style scoped>

</style>
