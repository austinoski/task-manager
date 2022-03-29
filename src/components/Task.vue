<template>
    <div @dblclick="this.$emit('toggle-reminder', task.id)" class="task" :class="{reminder: task.reminder}">
        <div>
            <h3>{{ task.text }}</h3>
            <p>{{ task.day }}</p>
        </div>
        <i id="delete" @click="this.$emit('delete-task', task.id)" class="fa fa-close"></i>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    }
}
</script>

<style scoped>
    .task {
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: lightgrey;
        padding: 0px 10px;
        padding-top: 5px;
    }
    .reminder {
        border-left: 10px solid green;
    }
    #delete {
        color: red;
    }
</style>
