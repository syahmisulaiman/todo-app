<template>
  <div id="app">
    <h1>To-Do List</h1>
    <div>
      <input 
        type="text" 
        v-model="newTask" 
        placeholder="Enter a new task" 
        @keyup.enter="addTask"
      />
      <button @click="addTask">Add</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :class="{ completed: task.completed }" @click="toggleComplete(index)">
          {{ task.text }}
        </span>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = "";
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 10px;
  padding: 5px 10px;
  cursor: pointer;
}
input {
  padding: 5px;
  width: 200px;
}
</style>
