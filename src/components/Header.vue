<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @toggle-add-task-form="this.$emit('toggle-add-task-form')" :text="showAddTaskForm ? 'Close' : 'Add Task'" :color="showAddTaskForm ? 'red' : 'green'" />
    </header>
</template>

<script>
import Button from "./Button.vue"

export default {
    name: "Header",
    components: {
        Button,
    },
    props: {
        title: String,
        showAddTaskForm: Boolean
    },
    emits: ['toggle-add-task-form']
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        padding: 5px 10px;
        margin: 20px auto;
        align-items: center;
        margin-bottom: 1px;
    }
</style>