<template>
    <header>
        <h1>{{title}}</h1>
        <ButtonComponent text="Add Task" color="green" />
        <ButtonComponent text="Update Task" color="blue" />
        <ButtonComponent text="Delete Task" color="red" />
    </header>
</template>



<script>
import ButtonComponent from './Button.vue';

export default {
    name : 'Header',
    props: {
        title:{
            type:String,
            default:'Hello world',
        },
    },
    components:{
        ButtonComponent
    }
} 
</script>


<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

</style>

