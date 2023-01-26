<template>
  <div class="container pt-5">
    <div class="todos form-control">
      <h1>Adicionar Tarefa</h1>
      <div class="content">
        <form class="row g-3">
          <div class="col-auto">
            <input
              type="text"
              class="form-control input-task"
              v-model="todoName"
              placeholder="Adicionar nova tarefa"
            />
          </div>
          <div class="col g-2">
            <i class="bi bi-file-plus-fill text-success" @click="addTask()"></i>
          </div>
        </form>
      </div>
    </div>
    <div >
    </div>
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
.container {
  max-width: 900px;
  margin: 0 auto;
  border-radius: 8px;
}

h1 {
  text-align: center;
}

.content {
  margin-left: 25%;
}

.done {
  text-decoration: line-through;
}

li {
  font-size: 18px;
  margin-top: 5px;
}

.input-task {
  width: 400px;
}

.bi-file-plus-fill,
.bi-check-square-fill,
.bi-trash3-fill {
  font-size: 35px;
  cursor: pointer;
}
</style>
