<template>
  <div id="app">
      <Header />
    <Tasks v-bind:tasks="tasks"  v-on:del-task="deleteTask"/>
  </div>
</template>

<script>

import Tasks from '../components/Tasks'
import Header from '../components/Header'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Tasks, Header
  }, 
  data(){
    return {
      tasks:[ ]
    }
  },
  methods:{
    deleteTask(taskId){
      axios.delete(`http://localhost:8083/task/${taskId}`)
      .then( () => this.tasks = this.tasks.filter(task => task.taskId !== taskId))
      .catch(err => console.log(err))
    }
  },
  created(){
    axios.get('http://localhost:8083/tasks')
    .then(res => this.tasks = res.data)
    .catch(err => console.log(err))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
