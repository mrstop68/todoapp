<template>
    <div>
       <h1> Todo List</h1>
       <TodoList/>
    </div>
</template>

<script>
import todoList from '../components/todoList.vue'
import TodoList from '../components/todoList.vue'
export default{
    name:"todoList",
    components:{
    todoList,
    TodoList
}
}
</script>