<template>
    <div>
        Listeye Ekle
        <div class="container">
            <input type="text" v-model="todoName" @keyup.enter="addTodo"  name="addTodo" id="addTodo">
            <input type="button" @click="addTodo" value="Ekle">
        </div>
        <ul class="todo">
            <li v-for="todo of todos" :key="todo.id">{{todo.title}}</li>
        </ul>
    </div>
</template>
<script>
import axios from "axios";
const url="http://localhost:3000/todos";
export default{
    name:"todoList",
    data(){
        return{
            todos:[],
            todoName:""
        }
    },
    async created() {
        try {
            const response = await axios.get(url);
            this.todos = response.data;
        } catch (error) {
            console.log(error);
        }
    },
    //promise yapısı ile de yapılabilir
    // created(){
    //     axios.get("http://localhost:3000/todos")
    //     axios.get("http://jsonplaceholder.typicode.com/todos")
    //     .then(response=>{
    //         this.todos=response.data;
    //     })
    // }
    methods:{
        async addTodo(){
            try {
                const response = await axios.post(url,{
                    title:this.todoName
                });
                this.todos.push(response.data);
                //veya
                // this.todos=[...this.todos,response.data];
                this.todoName="";
            } catch (error) {
                console.log(error);
            }
        }
    }
}
</script>
<style>
.todo{
    list-style-type: none;
    padding: 0;
    max-width: 360px;
    margin: 0 auto;
}
.todo li{
    border: 1px solid #42b983;
    margin: 10px;
    padding: 5px;
}
.container input[type="text"]{
    margin: 10px;
    padding: 5px;
    border: 1px solid #42b983;
}
.container input[type="button"]{
    margin: 10px;
    padding: 5px 20px;
    border: 1px solid #42b983;
}
  .container button{
    margin: 10px;
    padding: 5px 20px;
    border: 1px solid #d80000;
  }  
</style>