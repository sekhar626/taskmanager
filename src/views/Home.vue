<template>
    <AddTask v-show="showAddTask" @add-task='addTask'/>
    <Tasks @toggle-remainder="toggleRemainder"
    @delete-task="deleteTask" :tasks="tasks"
    />
</template>

<script>
import Tasks from '../components/Tasks.vue';
import AddTask from "../components/AddTask.vue";
export default {
    name:'Home',
    components:{AddTask,Tasks},
    props:{
        showAddTask:Boolean
    },

    data(){
        return{
            tasks:[]
        }
    },
    methods:{
    async deleteTask(id){
      if (confirm('are you sure?')){
        const res=await fetch(`http://localhost:8081/tasks/${id}`,{
          method:'DELETE',
        })
        res.status===200?(this.tasks=this.tasks.filter((task)=>task.id!==id)):alert('sorry couldnt delete')
      }
    },

    async toggleRemainder(id){
      console.log(id)
      const taskToToggle=await this.fetchTask(id)
      const updateTask={...taskToToggle,remainder:!taskToToggle.remainder}
      const res=await fetch(`http://localhost:8081/tasks/${id}`,{
        method:'PUT',
        headers:{
          'Content-type':'application/json'
        },
        body:JSON.stringify(updateTask)
      })
      const data=await res.json()
      this.tasks=this.tasks.map((task)=>task.id === id ? {...task,remainder:data.remainder}:task)
    },

    async addTask(task){
      const res=await fetch('http://localhost:8081/tasks',{
        method:'POST',
        headers:{
          'Content-type':'application/json'
        },
        body:JSON.stringify(task)
      })
      const data=await res.json()

      this.tasks=[...this.tasks,data]
    },

    async fetchTasks(){
      const res=await fetch('http://localhost:8081/tasks')
      const data=await res.json()

      return data
    },
    async fetchTask(id){
      const res=await fetch(`http://localhost:8081/tasks/${id}`)
      const data=await res.json()

      return data
    }
  },
  async created(){
    this.tasks=await this.fetchTasks()
  },
  emits:['delete-task','toggle-remainder','add-task']
}
</script>