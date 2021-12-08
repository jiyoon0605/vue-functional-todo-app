<template>
  <div id="app">
    <TodoHeader/>
    <TodoInput v-on:addTodo="addTodo"/>
    <TodoList v-bind:todoItems="todoItems" v-on:removeTodo="removeTodo" v-on:toggleComplete="toggleComplete"/>
    <TodoFooter v-on:clearAll="clearAll"/>
  </div>
</template>

<script>

import TodoHeader from "@/components/TodoHeader";
import TodoList from "@/components/TodoList";
import TodoInput from "@/components/TodoInput";
import TodoFooter from "@/components/TodoFooter";

export default {
  data: function () {
    return {
      todoItems: []
    }
  },
  methods: {
    addTodo: function (newTodoItem) {
      const obj = {
        completed: false,
        item: newTodoItem
      };
      localStorage.setItem(newTodoItem, JSON.stringify(obj));
      this.readTodos();
    },
    removeTodo: function (item, index) {
      localStorage.removeItem(item);
      this.todoItems.splice(index, 1);
    },
    toggleComplete: function (item) {
      item.completed = !item.completed;
      localStorage.removeItem(item.item);
      localStorage.setItem(item.item, JSON.stringify(item));
    },
    clearAll: function () {
      localStorage.clear();
      this.readTodos();
    },
    readTodos: function () {
      this.todoItems = [];
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
    }
  },
  created: function () {
    this.readTodos();
  },
  components: {
    TodoHeader,
    TodoList,
    TodoInput,
    TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
