<template>
  <div class="app">
    <header class="app-header">
      <h1>To do list!</h1>
    </header>
    <add-task-form @add-task="addNewTask"></add-task-form>
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

  provide() {
    return {
      deleteTask: this.deleteTask,
      changePriority: this.changePriority
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
  },

  methods: {
    addNewTask(newTask) {
      const arrayWithNewTask = this.tasks;
      arrayWithNewTask.unshift(newTask);

      this.tasks = arrayWithNewTask;
    },

    deleteTask(id) {
      const tasksAfterRemoveDeltedOne = this.tasks.filter(task => task.id !== id);
      this.tasks = tasksAfterRemoveDeltedOne;
    },

    changePriority(id) {
      const tasksArrayAfterChangingPriority = this.tasks.map(task => {
        if(task.id === id) {
          const prevValue = task.isImportant;
          task.isImportant = !prevValue;
        }
        return task
      });

      console.log(tasksArrayAfterChangingPriority);

      this.tasks = tasksArrayAfterChangingPriority;
    }
  }
}
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.app-header {
  width: 100%;
  padding: 10px;
  margin-bottom: 50px;
  text-align: center;
  background: #658864;
  color: rgb(233, 230, 230);
}
</style>
