<template>
    <div class="todo-list-container">
      <h1>TO-DO LIST</h1>
      <form @submit.prevent="addActivity">
        <input type="text" v-model="newActivity" placeholder="Add activity...">
        <button>Add</button>
      </form>
      <ul>
        <li v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.completed }">
          <input type="checkbox" v-model="activity.completed">
          <span>{{ activity.text }}</span>
          <button class="remove-button" @click="removeActivity(index)">Remove</button>
        </li>
      </ul>
      <div>
        <label>Show only unfinished activities:</label>
        <input type="checkbox" v-model="showUnfinished">
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {return {
        newActivity: '',
        activities: [
          { text: 'Buy groceries', completed: false },
          { text: 'Finish homework', completed: true },
          { text: 'Clean the house', completed: false }
        ],
        showUnfinished: false
      }
    },
    methods: {
      addActivity() {
        if (this.newActivity.trim() !== '') {
          this.activities.push({ text: this.newActivity, completed: false });
          this.newActivity = '';
        }
      },
      removeActivity(index) {
        this.activities.splice(index, 1);
      }
    },
    computed: {
      filteredActivities() {
        if (this.showUnfinished) {
          return this.activities.filter(activity => !activity.completed);
        } else {
          return this.activities;
        }
      }
    }
  }
  </script>
  
  <style>
  .todo-list-container {
    max-width: 500px;
    margin: auto;
    padding: 20px;
    background-color: #f5f5f5;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
  }
  
  h1 {
    text-align: center;
    color: #4a4a4a;
  }
  
  form {
    display: flex;
    margin-bottom: 20px;
  }
  
  form input[type="text"] {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px 0 0 5px;
    border: none;
  }
  
  form button {
    padding: 10px;
    font-size: 16px;
    border: none;
    border-radius: 0 5px 5px 0;
    background-color: #2ecc71;
    color: #fff;
    cursor: pointer;
  }
  
  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  li {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }
  
  li input[type="checkbox"] {
    margin-right: 10px;
    cursor: pointer;
  }
  
  li span {
    flex: 1;
    color: #4a4a4a;
    font-size: 16px;
  }
  
  li button.remove-button {
    background-color: #e74c3c;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    margin-left: 10px;
    cursor: pointer;
  }
  </style>
  