<template>
    <ul class="tasks-list">
        <one-task v-for="task in tasks" :text="task.text" :id="task.id" :key="task.id" :is-important="task.isImportant"></one-task>
    </ul>
</template>
<script>
import OneTask from './OneTask.vue';

export default {
    name: 'TasksList',
    components: { OneTask },

    props: {
        tasks: {
            type: Array,
            required: true
        }
    }
}
</script>
<style>
    
</style>