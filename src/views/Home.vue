<template>
    <div class="inner-box">
      <AddTask v-show="showAddTaskForm" @add-task="addTask" />
      <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
</template>

<script>
import AddTask from "../components/AddTask.vue"
import Tasks from "../components/Tasks.vue"

export default {
    name: "Home",
    components: {
        Tasks,
        AddTask,
    },
    props: {
        showAddTaskForm: Boolean
    },
    data() {
        return {
            tasks: []
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
  }
}
</script>

<style scoped>
  .inner-box {
    margin: 13px;
  }
</style>
