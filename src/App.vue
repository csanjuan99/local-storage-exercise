<template>
  <div>
    <h1>
      Administrador de tareas
    </h1>
    <h2> {{ name }}</h2>
    <div>
      <input type="text" placeholder="Titulo de la tarea" v-model="newTask.title">
      <input type="number" placeholder="Horas" v-model="newTask.time">
      <button @click="addTask">Guardar</button>
      <button @click="cancelTask">Cancelar</button>
    </div>
    <div>
      <template v-if="tasks.length > 0">
        <ul>
          <li v-for="(task, i) in tasks" :key="i">
          <span>
            {{ task.title }} - {{ task.time }} horas
          </span>
            <button @click="removeTask(i)">Eliminar</button>
          </li>
        </ul>
      </template>
      <template v-else>
        <p>
          No hay tareas
        </p>
      </template>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    name: 'Carlos Daniel Sanjuan',
    tasks: [],
    newTask: {
      title: '',
      time: 0
    }
  }),
  mounted() {
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
              title: this.newTask.title,
              time: this.newTask.time
            }
        );
        localStorage.setItem("tasks", JSON.stringify(this.tasks))
      }
      this.newTask = {
        title: '',
        time: 0
      };
    },
    cancelTask() {
      this.newTask = {
        title: '',
        time: 0
      };
    },
    removeTask(i) {
      this.tasks.splice(i, 1);
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
