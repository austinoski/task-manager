<template>
        <div class="tasks" :key="task.id" v-for="task in tasks">
            <Task @toggle-reminder="this.$emit('toggle-reminder', task.id)" @delete-task="this.$emit('delete-task', task.id)" :task="task" />
        </div>
</template>

<script>
import Task from "./Task.vue"

export default {
    name: "Tasks",
    props: {
        tasks: Array
    },
    emits: ['delete-task', 'toggle-reminder'],
    components: {
        Task
    }
}
</script>

<style scoped>
.tasks {
    border: 1px solid black;
    margin: 10px auto;
}
</style>
