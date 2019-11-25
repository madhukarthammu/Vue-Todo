

<template>
  <div class="home">
  <h2>Vue Todo List</h2>

  <div class="input-group mb-3">
  <input type="text" required v-model="newtask" @keyup.enter="addtodo()" class="form-control additem" placeholder="Add a Todo" aria-label="Recipient's username" aria-describedby="basic-addon2">
    <div class="input-group-append">
  <button class="btn btn-primary" id="basic-addon2" v-on:click="addtodo()">Add Todo</button>
    </div>
  </div>
 
 
<div class="wrapper">
  <div style="float: left; margin-left: 15px">
   <input type="checkbox" @click="toggleSelect" :checked="selectAll"/>
  <label style="padding-left: 10px">Tasks are done</label>
  </div>
  <div style="float:right">
       <p class="clearList" style="cursor: pointer; margin-right: 20px;" @click="clearall">ClearList</p>
    </div>
 
   <ul class="todolist">
      <li v-for="(todo, index) in todos" :key="index" :class="[{ 'active': todo.completed }]" >
      <span>{{ todo.text }} </span>
      <input type="checkbox" @click="completedtask(todo)" v-model="todo.completed" class="checkbox" />
      <div class="edit">
      <button class="btn remove" v-on:click="removetodo(todo)">X</button>
        </div>  
</li>
<hr />
<div class="row">
<div class="numberofTodos col-md-6 text-left">
 <p>Tasks Done:{{remaining}}</p>
</div>

</div>
</ul>

</div>
  </div>
</template>

<script>
// @ is an alias to /src
 var filters = {
    active: function(todos) {
      return todos.filter(function(todo) {
        return todo.completed;
      })
    }
  }

export default {
  name: 'home',
   data () {
        return{
         todos: [
           { text: 'wake up early', completed: false },
           { text: 'Learn Vue',  completed: false}
         
          ],
         newtask: ""
        
        }
    },

  methods: {
   addtodo() {
     const addvalue = this.newtask.trim();
     this.todos.push({text: addvalue,  completed: false});
     this.newtask = "";
    },

    removetodo(todo) {
        var index = this.todos.indexOf(todo);
				this.todos.splice(index, 1);
   },

    clearall() {
      this.todos = [];
    },

    completedtask(todo){
      todo.completed = !todo.completed
    },
      toggleSelect: function() {
        debugger
      var select = this.selectAll;
      this.todos.forEach(function(todo) {
        todo.completed = !select;
      });
      this.selectAll = !select;
    },
    },

    computed: {
    selectAll: function() {
      return this.todos.every(function(todo){
        return todo.completed;
      });
    },
    remaining: function() {
      return filters.active(this.todos).length;
    }
  },
 
  }



</script>

<style scoped>
.numberofTodos{
  float: left;
}

.remove{
  border: 1px solid;
}

.remove:hover{
  background: #000;
  color: #fff;
}

.input-group{
  width: 20%;
  text-align: center;
  margin: 0 auto;
}

.todolist{
  margin-top: 30px;
}

.all li{
  display: inline-block;
  padding-top: 0 !important;
  cursor: pointer;
  color: #aaa;
}

ul{
    margin: 0;
    padding: 0;
}

.todolist li{
    padding: 12px;


    list-style-type: none;
    border-radius: 5px;

}

.todolist li .edit{
    float: right;
    margin-right: 50px;
}

.todolist li .edit .btn{
    margin: 0px -30px 30px 0px;
}

.active{
  text-decoration: line-through;
}

span{
  font-size: 30px;
}

.wrapper{
  width: 30%;
  margin: 0 auto;
  border: 1px solid #eee;
  margin-top: 50px;
  background: #fff;
  padding: 20px 15px 0px;

	position: relative;
  border-radius: 10px;
	box-shadow: 0 0 13px rgba(0, 0, 0, 0.2)
}

.checkbox{
      float: left;
    width: 20px;
    height: 30px;
    margin-top: 8px;
}
</style>