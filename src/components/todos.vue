<template>
    <div>

        <div v-bind:key="todo.id" v-for="todo in todosy">
    <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
 
        </div>
    </div>
</template>



<script>
import TodoItem from './TodoItem';
export default {
    name : 'todos',
    components:{
    TodoItem
    },
props:["todosy"]
    
}
</script>




<style scoped>



</style>