<template>
  <div id="app">
    <h1>This is my todo List with Vue</h1>
    <input type="text" v-model = "newItem" @keyup.enter="addTodo">
    <button v-on:click="addTodo">+ Add</button>
    <button @click = "allDone">All done!</button>
    <ol>
      <li v-for = "todoItem in todos" >
            <span  
             :class="{isCompleted: todoItem.completed, incomplete: !todoItem.completed}">
             {{ todoItem.todoText }}
             </span>
            <button @click="deleteTodo(todoItem)">Smash it!</button>
            <button v-if = "!todoItem.completed" @click="completeTodo(todoItem)">I did it!</button>
          <button v-if = "todoItem.completed" @click="completeTodo(todoItem)">I didn't do it</button>
      </li>
    </ol>
  </div>
</template>

<script>

export default {
  data() {
    return {
      todos:[],
      todo: {
        todoText: '',
        completed: false,
      },
      newItem: '',
    }
    },
  methods: {
    addTodo: function () {
      this.todos.push({
        todoText: this.newItem,
        completed: false,
      });
      this.newItem = '';
    },
    deleteTodo: function (todoItem) {
      let todoIndex = this.todos.indexOf(todoItem);
      this.todos.splice(todoIndex, 1);
    },
    completeTodo: function(todoItem) {
      let todoIndex = this.todos.indexOf(todoItem);
      this.todos[todoIndex].completed = !this.todos[todoIndex].completed;
    },
    allDone: function () {
      this.todos.forEach((todoItem) => {
        todoItem.completed = !todoItem.completed
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

button{
  margin: 5px;
}

.isCompleted {
    color: green;
  }

.incomplete {
  color: black;
}
</style>
