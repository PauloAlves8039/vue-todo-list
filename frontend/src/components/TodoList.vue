<template>
  <div class="container pt-5">
    <div class="todos form-control">
      <h2 class="title-task">Adicionar Tarefa</h2>
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
    <div class="container-task py-3">
      <h2 class="title-task">Tarefas</h2>
      <table class="table table-hover table-bordered">
        <thead class="table-dark text-center">
          <tr>
            <th>Nome</th>
            <th>Ação</th>
          </tr>
        </thead>
        <tbody v-for="(todo, index) in todos" :key="index" :class="{ done: todo.done }">
          <tr>
            <td>{{ todo.name }}</td>
            <td class="actions">
              <i
                @click="completeTask(todo.id)"
                class="bi bi-check-square-fill px-md-1 text-primary"
              ></i>
              <i
                @click="removeTask(todo.id)"
                class="bi bi-trash3-fill px-md-1 m-1 text-danger"
              ></i>
            </td>
          </tr>
        </tbody>
      </table>
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
      this.clearFild();
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
    },
    clearFild() {
      this.todoName = "";
    },
  }
}
</script>

<style scoped>
.container {
  max-width: 900px;
  margin: 0 auto;
  border-radius: 8px;
}

.title-task {
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

.bi-file-plus-fill {
  font-size: 35px;
}

.bi-check-square-fill,
.bi-trash3-fill {
  font-size: 25px;
}

.bi-file-plus-fill,
.bi-check-square-fill,
.bi-trash3-fill {
  cursor: pointer;
}

.actions {
  width: 150px;
  text-align: center;
}
</style>
