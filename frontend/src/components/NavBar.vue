<template>
    <div class="container-fluid">
        <div class="row flex-nowrap">
            <div class="col-auto col-md-3 col-xl-2 px-sm-2 px-0 bg-dark">
                <div class="d-flex flex-column align-items-center align-items-sm-start px-3 pt-2 text-white min-vh-100">
                    <a href="/" class="d-flex align-items-center pb-3 mb-md-0 me-md-auto text-white text-decoration-none">
                        <span class="fs-5 d-none d-sm-inline">Lista de Tarefas</span>
                    </a>
                    <ul class="nav nav-pills flex-column mb-sm-auto mb-0 align-items-center align-items-sm-start" id="menu">
                        <li class="nav-item">
                            <a href="#" class="nav-link align-middle px-0">
                                <i class="fs-4 bi-house"></i> <span class="ms-1 d-none d-sm-inline">Início</span>
                            </a>
                        </li>
                    </ul>
                    <hr>
                    <div class="dropdown pb-4">
                        <a href="https://github.com/PauloAlves8039" target="_blank"
                            class="d-flex align-items-center text-white text-decoration-none" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            <img src="https://avatars.githubusercontent.com/u/57012714?v=4" alt="hugenerd" width="30"
                                height="30" class="rounded-circle">
                            <span class="d-none d-sm-inline mx-1">Paulo Alves</span>
                        </a>
                    </div>
                </div>
            </div>
            <div class="col py-3">
                <TodoList />
            </div>
        </div>
    </div>
</template>
  
<script>
import TodoList from '@/components/TodoList.vue'

export default {
    name: 'NavBar',
    components: {
        TodoList
    }
};
</script>
  
<style scoped>
.nav-link {
  color: #06EEFF;
}

.nav-link:hover {
  color: #AB82FF;
}
</style>
  