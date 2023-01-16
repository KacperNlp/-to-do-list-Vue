<template>
    <div>
        <form @submit="handleSubmitForm">
            <input type="text" v-model="taskText">
            <input type="checkbox" v-model="isImportant">
            <button>Add task!</button>
        </form>
    </div>
</template>
<script>
const MAX_VALUE_OF_INDER = 100000;
const generateRandomId = () => {
    return Math.floor(Math.random() * MAX_VALUE_OF_INDER);
}

export default {
    name: 'AddTaskForm',
    emits: ['add-task'],

    data() {
        return {
            taskText: '',
            isImportant: false
        }
    },

    methods: {
        handleSubmitForm(e) {
            e.preventDefault();
            
            const { taskText, isImportant } = this;
            const idOfGeneratedTask = generateRandomId();
            const newTask = {
                text: taskText,
                isImportant,
                id: idOfGeneratedTask
            };

            if(this.checkIfTaskIsAddedCorrectly(newTask)) {
                alert("Sorry you didn't set value of your task or we cannot generate ID");
                return;
            }

            this.resetForm();
            this.$emit('add-task', newTask);
        },

        resetForm() {
            this.taskText = '';
            this.isImportant = false;
        },

        checkIfTaskIsAddedCorrectly(newTask) {
            const { text, id } = newTask;

            if(!text || !id) return true;
            return false;
        }
    }
}
</script>
<style>
    
</style>