<template>
  <div class="box">
    <Header :showAddTaskForm="showAddTaskForm" @toggle-add-task-form="toggleAddTaskForm" title="Task Tracker"/>
    <div class="inner-box">
      <AddTask v-show="showAddTaskForm" @add-task="addTask" />
      <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import AddTask from "./components/AddTask.vue"
import Tasks from "./components/Tasks.vue"
import Footer from "./components/Footer.vue"

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
    Footer,
  },
  data() {
    return {
      tasks: [],
      showAddTaskForm: false
    }
  },
  methods: {
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
        headers: {
          "Content-type": "application/json"
        }
      })
      
      res.status === 200 ? (this.tasks = this.tasks.filter(
        (task) => task.id !== id)) : alert("Error Deleting Task");

    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)

      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(updateTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map((task) => task.id === id ?
      {...task, reminder: data.reminder} : task)
    },
    async addTask(newTask) {
      const res = await fetch('api/tasks', {
        method: "POST",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(newTask)
      })
      
      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    toggleAddTaskForm() {
      this.showAddTaskForm = !this.showAddTaskForm
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()

      return data
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
}
</script>

<style>
  .box {
    border: 3px solid black;
    border-radius: 5px;
    margin: 5px;
  }
  .inner-box {
    margin: 13px;
  }
  #app {
    font-size: 1rem;
  }
</style>
