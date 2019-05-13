<template>
<div class="todo-main">
      <h3>Todo App</h3>
        <input type="text" placeholder="Add todo" ref="myTodo"  />
        <button v-if="!edit" v-on:click="handleAdd">Add task</button>
        <button v-else v-on:click="handleEdited">Edit Task</button>
      <div class="showTodo">
        <ul>
          <li v-for="(todo,i) in todos" :key="i">
              {{todo}}
             <button class="editButton" v-on:click="handleEdit(todo, i)">Edit</button>
            <button class="deleteButton" v-on:click="getIndex(i)">Delete</button>
          </li>
        </ul>
        <Search></Search>
      </div>
      </div>
</template>

<script>
import Search from '../src/components/Search.vue';
module.exports = {
  data: function() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [], 
      edit: false, 
      index: ''
      }
  }, 
  methods: {
    handleAdd: function() {
        let newTodo = this.$refs.myTodo.value

        if(newTodo == '') {
          alert('Add a todo')
        } else {
          this.todos.push(this.$refs.myTodo.value)
          localStorage.setItem("todos", JSON.stringify(this.todos))
          this.$refs.myTodo.value = ''
        }
    },
    getIndex: function(i) {
      this.todos.splice(i,1)
      localStorage.setItem("todos", JSON.stringify(this.todos))
    }, 
    handleEdit: function(todo, i) {
      this.edit = true
      this.index = i
      this.$refs.myTodo.value = todo
    }, 
    handleEdited: function(i) {
      this.edit = false
      this.todos[this.index] = this.$refs.myTodo.value
      localStorage.setItem("todos", JSON.stringify(this.todos))
      this.$refs.myTodo.value = ''
      this.index = ''
    }
  }
}
</script>


<style>
.todo-main {
  text-align: center
}

li {
  list-style-type: none
}
</style>

