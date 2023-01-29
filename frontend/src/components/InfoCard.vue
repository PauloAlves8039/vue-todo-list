<template>
  <div class="card" style="width: 18rem">
    <div class="card-body">
      <h5 class="card-title">Total de tarefas</h5>
      {{ countTodo }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    countTodo: [],
  },
};
</script>

<style scoped>
</style>
