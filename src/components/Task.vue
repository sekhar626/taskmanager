<template>
    <div @dblclick="$emit('toggle-remainder',task.id)"
     :class="[task.remainder?'remainder':'','task']">
        <h3>
            {{task.text}}
            <i class="fas fa-times" @click="$emit('delete-task',task.id)"></i>
        </h3>
        <h3>{{task.day}}</h3>
    </div>
    
</template>

<script>
export default {
    name:'Task',
    props:{
        task:Object
    },
    
}
</script>

<style scoped>
    .task{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        background: #f4f4f4;
        margin: 5px;
    }
    .remainder{
        border-left:5px solid green;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        background: #f4f4f4;
        margin: 5px;
    }
    h3{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0px;
    }
    .fas{
        color: red;
    }
</style>