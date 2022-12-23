<template>
    <div :key="task.id" v-for="task in tasks">
        <Task v-on:delete-task="$emit('delete-task',task.id)" :task="task"/>
    </div>
</template>

<script>
import Task from './Task.vue'

export default{
    name:'TasksComponent',
    props:{
        tasks:Array,
    },
    components:{
        Task
    },
    emits:['delete-task']
}
</script>