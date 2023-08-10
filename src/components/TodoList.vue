<template>
  <div>
    <input v-model="newTask" placeholder="Enter a new task" />
    <button @click="addTask">Add Task</button>
    
    <div>
      <button @click="toggleFilter('all')">All</button>
      <button @click="toggleFilter('completed')">Completed</button>
      <button @click="toggleFilter('uncompleted')">Uncompleted</button>
    </div>

    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'all'
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      } else if (this.filter === 'uncompleted') {
        return this.tasks.filter(task => !task.completed);
      } else {
        return this.tasks;
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleFilter(filter) {
      this.filter = filter;
    }
  }
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
