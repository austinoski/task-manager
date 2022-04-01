<template>
  <div class="box">
    <Header :showAddTaskForm="showAddTaskForm" @toggle-add-task-form="toggleAddTaskForm" title="Task Tracker"/>
    <router-view :showAddTaskForm="showAddTaskForm"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Home from './views/Home.vue'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Home,
  },
  data() {
    return {
      showAddTaskForm: false
    }
  },
  methods: {
    toggleAddTaskForm() {
      this.showAddTaskForm = !this.showAddTaskForm
    }
  }
}
</script>

<style>
  .box {
    border: 3px solid black;
    border-radius: 5px;
    margin: 5px;
  }
  #app {
    font-size: 1rem;
  }
</style>
