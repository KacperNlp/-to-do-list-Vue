<template>
  <div class="app">
    <add-task-form></add-task-form>
    <tasks-list></tasks-list>
  </div>
</template>

<script>
import AddTaskForm from './components/AddTaskForm.vue';
import TasksList from './components/TasksList.vue';

export default {
  name: 'App',
  components: { AddTaskForm, TasksList }
}
</script>

<style>
</style>
