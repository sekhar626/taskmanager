<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-task')" :text="showAddTask? 'close' : 'add Task'" :color="showAddTask?'red' : 'green'"/>
    </header>
</template>


<script>
import Button from "./Button.vue";

export default {
    name:'Header',
    props:{
        title:String,
        showAddTask:Boolean
    },
    components:{
        Button
    },
    computed:{
        homePage(){
            if(this.$route.path==='/'){
                return true
            }else{
                return false
            }
        }
    }
}

</script>

<style scoped>
header{
    font-family: 'sans-serif';
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;

}
</style>