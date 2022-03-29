<template>
    <button @click.prevent="this.$emit('toggle-add-task-form')" class="btn" :style="{background: color}">
        {{ text }}
    </button>
</template>

<script>
    export default {
        name: "Button",
        props: {
            text: String,
            color: String
        }
    }
</script>

<style scoped>
    button {
        color: white;
    }
    button:focus {
        box-shadow: none;
    }
</style>
