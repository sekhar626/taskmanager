<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label>Task</label>
            <input type="text" v-model="text" name="text" placeholder="Add Task"/>
        </div>
        <div class="form-control">
            <label>Day & Time</label>
            <input type="text" name='day' v-model="day" placeholder="Add Day & Time"/>
        </div>
        <div class="form-control form-control-check">
            <label >Set Remainder</label>
            <input type="checkbox" v-model="remainder" name='remainder' />
        </div>
        <input type="submit" value="Save Task" class="btn btn-block"/>
    </form>
</template>

<script>
export default {
    name:'AddTask',
    data(){
        return{
            text:'',
            day:'',
            remainder:false
        }
    },
    methods:{
        onSubmit(event){
            event.preventDefault()
            if(!this.text){
                alert('please add text')
                return
            }
            const newTask={
                id:Math.floor(Math.random()*100000),
                text:this.text,
                day:this.day,
                remainder:this.remainder
            }

            this.$emit('add-task',newTask)

            this.text="",
            this.day="",
            this.remainder=false

            console.log(newTask)

        }
    }

}
</script>

<style scoped>
    .add-form{
        margin-bottom: 40px;
    }
    .form-control{
        margin: 20px 0px;
    }
    .form-control label{
        display: block;
        align-items: flex-start;
    }
    .form-control input{
        width: 100%;
        height: 32px;
        margin: 5px;
        padding: 3px 7px;
        font-size: 18px;
    }
    .form-control-check{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .form-control-check label{
        flex: 1;
    }
    .form-control-check input{
        flex: 2;
        height: 20px;
    }
</style>