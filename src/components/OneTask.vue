<template>
    <p>{{ text }}</p>
</template>
<script>
export default {
    name: 'OneTask',
    props: {
        text: {
            type: String,
            required: true
        },
        id: {
            type: Number,
            required: true
        }
    }
}
</script>
<style>
    
</style>