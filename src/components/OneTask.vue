<template>
    <li class="task">
        <p>{{ text }}</p>
        <p v-if="isImportant">This ticket is IMPORTANT!</p>
        <button @click="handleDeleteTask">Delete</button>
        <button @click="handleChangePriority">Change Priority!</button>
    </li>
</template>
<script>
export default {
    name: 'OneTask',
    inject: ['deleteTask', 'changePriority'],

    props: {
        text: {
            type: String,
            required: true
        },
        id: {
            type: Number,
            required: true
        },
        isImportant: {
            type: Boolean,
            default: false
        }
    }, 

    methods: {
        handleDeleteTask() {
            this.deleteTask(this.id);
        },

        handleChangePriority() {
            this.changePriority(this.id);
        }
    }
}
</script>
<style>
    
</style>