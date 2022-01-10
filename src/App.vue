<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTasks" :showAddTask="showAddTask" title="Task Manager"/>
    
    <router-view :showAddTask='showAddTask'></router-view>
    <Footer />
  </div>
  
</template>

<script>

import Header  from "./components/Header.vue";

import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,Footer
  },
  data(){
    return {
      
      showAddTask:false
    }
  },
  methods:{
    toggleAddTasks(){
      this.showAddTask=!this.showAddTask
    },
  },
  emits:['delete-task','toggle-remainder','add-task']

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

body{
  font-family: sans-serif;
}

.container{
  max-width: 600px;
  margin: 30px auto;
  overflow: auto;
  min-height: 400px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn{
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
}
</style>
