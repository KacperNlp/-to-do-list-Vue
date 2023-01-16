<template>
  <div class="app">
    <add-task-form></add-task-form>
    <tasks-list v-if="isTasksNotEmpty" :tasks="tasks"></tasks-list>
    <message-component v-else></message-component>
  </div>
</template>

<script>
import AddTaskForm from './components/AddTaskForm.vue';
import MessageComponent from './components/MessageComponent.vue'
import TasksList from './components/TasksList.vue';

export default {
  name: 'App',
  components: { AddTaskForm, MessageComponent, TasksList },

  data() {
    return {
      tasks: []
    }
  },

  computed: {
    isTasksNotEmpty() {
      return !!this.tasks.length;
    }
  },

  beforeMount() {
    fetch('./tasks.json')
      .then(res => {
        if(res.ok) return res.json();
        throw new Error(`Wrong status: ${res.status}`);
      }).then(res => {
        this.tasks = res.tasks;
      }).catch(err => {
        throw new Error(err);
      })
  }
}
</script>

<style>
</style>
