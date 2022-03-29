<template>
    <form action="" method="post">
        <div>
            <textarea class="form-control" name="text" v-model="text" placeholder="Task Description..." />
        </div>
        <div>
            <input class="form-control datepicker" type="text" name="day" v-model="day" placeholder="Task Date..." />
        </div>
        <div class="form-check">
            <input class="form-check-input" type="checkbox" name="reminder" v-model="reminder" id="reminder" />
            <label class="form-check-label" for="reminder">Reminder</label>
        </div>
        <input @click.prevent="addTask" class="form-control btn btn-secondary" type="submit" value="Submit" />
    </form>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            text: "",
            day: "",
            reminder: false,
            newTask: {}
        }
    },
    methods: {
        addTask() {
            this.newTask = {
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }
            this.$emit('add-task', this.newTask)
            this.resetFormValues()
        },
        resetFormValues() {
            this.text = ""
            this.day = ""
            this.reminder = false
        }
    }
}
</script>

<style scoped>
    form {
        margin-bottom: 60px;
    }
    input {
        margin: 5px auto;
    }
</style>
