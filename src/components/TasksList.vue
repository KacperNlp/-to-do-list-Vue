<template>
    <ul class="tasks-list"></ul>
</template>
<script>
export default {
    name: 'TasksList',
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