<template>
  <h1>{{ todo }}</h1>
  <div class="container">
        <div class="form">
            <input v-model.trim="todo" @keyup.enter="addTodo" type="text" class="input" />
            <input v-if="currentTodo === null" @click="addTodo" type="submit" class="add" value="Add Task" />
            <input v-else @click="updateTodo" type="submit" class="add" value="Update Task" />
        </div>
        
     <div v-if="todos.length">
        <div 
        v-for="(item,idx) in todos"
        :key="idx" 
        class="tasks"
        style="display: flex; align-items:center; justify-content:space-between"
        >
<div>
    <input v-model="item.checkbox" type="checkbox">
    <label 
    for="item"
    :class="item.checkbox ? 'decoration': ''"
    >
      {{item.title}}
    </label>
</div>
       
        <button @click="deleteItem(item)" class="del">Delete</button>
        <button @click="editTodo(idx)" class="del">Edit</button>   
    </div>
    <div @click="deleteAll" class="delete-all">Delete all</div>
    <div @click="deleteChecked" class="delete-all">Delete checked</div>
     </div>

     <div v-else>
        <img alt="Image Not Available icon" srcset="https://img.icons8.com/ios-filled/512/image-not-avialable.png 2x, https://img.icons8.com/ios-filled/256/image-not-avialable.png 1x" src="https://img.icons8.com/ios-filled/512/image-not-avialable.png" style="width: 256px; height: 256px; filter: invert(0%) sepia(96%) saturate(0%) hue-rotate(69deg) brightness(108%) contrast(104%);">
     </div>
    
        </div>

       
</template>

<script>


export default {
    name: "App",
    data() {
        return {
            title: "Todo APP",
            todo: "",
            currentTodo: null,
            todos: []
        };
    },
    methods: {
        addTodo() {
            if (this.todo.trim()) {
                this.todos.push({
                    title: this.todo,
                    id: Math.floor(Math.random() * 1000),
                    checkbox:false
                });
                this.todo = "";
            }
        },
        editTodo(idx){
            this.currentTodo = idx
            this.todo = this.todos[idx].title
        },
        updateTodo(){
            if(this.todo){
                this.todos[this.currentTodo].title = this.todo
           this.todo = ''
           this.currentTodo = null
            }
        },
        deleteItem(idx) {
            this.todos.splice(idx, 1);
        },
        deleteAll() {
            this.todos = [];
        },
        deleteChecked(){
            for(var i = 0; i<this.todos.length;i++){
                if(this.todos[i].checkbox){
                    this.todos.splice(i,1)
                }
            }
        }
    },
  
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
body {
            font-family: Arial, Helvetica, sans-serif;
        }
        .container {
            width: 500px;
            margin: 20px auto;
        }
        .form {
            background-color: #eee;
            border-radius: 6px;
            padding: 20px;
            display: flex;
            align-items: center;
        }
        .input {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 6px;
            flex: 1;
        }
        .input:focus , .add:focus{
            outline: none;
        }
        .add {
            border: none;
            background-color: #f44336;
            color: white;
            padding: 10px;
            border-radius: 6px;
            margin-left: 10px;
            cursor: pointer;
        }
        .tasks {
            background-color: #eee;
            margin-top: 20px;
            border-radius: 6px;
            padding: 20px;
        }
        .tasks .task {
            background-color: white;
            padding: 10px;
            border-radius: 6px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: 0.3s;
            cursor: pointer;
            border: 1px solid #ccc;
        }
        .tasks .task:not(:last-child) {
            margin-bottom: 15px;
        }
        .tasks .task:hover {
            background-color: #f7f7f7;
        }
        .tasks .task.done {
            opacity: 0.5;
            position: relative;
        }
        .task.done::after {
            position: absolute;
            content: "";
        }
        .tasks .task span { 
            font-weight: bold;
            font-size: 10px;
            background-color: red;
            color: white;
            padding: 2px 6px;
            border-radius: 4px;
            cursor: pointer;
        }
        .delete-all {
            width: calc(100% - 25px);
            margin: auto;
            padding: 12px;
            text-align: center;
            font-size: 14px;
            color: white;
            background-color: #f44336;
            margin-top: 20px;
            cursor: pointer;
            border-radius: 4px;
        }
        .del{
          background-color: #f44336;
          padding: 12px 20px;
            text-align: center;
            font-size: 14px;
            color: white;
            border: none;
            outline: none;
            border-radius: 10px; 
        }
        .decoration{
            text-decoration: line-through;
        }
</style>