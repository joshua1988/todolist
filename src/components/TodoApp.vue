<template>
  <div id="todoapp">
    <section class="todoapp">
      <header class="header">
        <h1>todos</h1>
        <input
          class="new-todo"
          placeholder="What needs to be done?"
          autofocus
          v-model="todoInput"
          v-on:keyup.enter="addTodo"
        >
      </header>
      <!-- This section should be hidden by default and shown when there are todos -->
      <Container
        v-bind:filteredTodoList="filteredTodoList"
        v-bind:filterStatus="filterStatus"
        v-bind:leftItems="leftItems"
        v-on:toggleCheck="toggleCheck"
        v-on:destroyTodo="destroyTodo"
        v-on:toggleAll="toggleAll"
        v-on:clearCompleted="clearCompleted"
        v-on:adjustFilter="adjustFilter"
      />
    </section>
    <footer class="info">
      <p>Double-click to edit a todo</p>
      <!-- Remove the below line ↓ -->
      <p>Template by
        <a href="http://sindresorhus.com">Sindre Sorhus</a>
      </p>
      <!-- Change this out with your name and url ↓ -->
      <p>Created by
        <a href="http://todomvc.com">you</a>
      </p>
      <p>Part of
        <a href="http://todomvc.com">TodoMVC</a>
      </p>
    </footer>
  </div>
</template>

<script>
import Container from './Container.vue'
import { Filter } from "../constants/filter";

export default {
  name: 'TodoApp',
  components: { Container },
  data() {
    return {
      todoInput: '',
      todoList: [{
        title: 'Make an application',
        checked: false 
      }, {
        title: 'Test an application',
        checked: false 
      }],
      filterStatus: Filter.ALL,
    }
  },
  methods: {
    addTodo: function addTodo () {
      if(this.todoInput == ''){
        return
      }
      this.todoList.push({
        title: this.todoInput,
        checked: false
      });
      this.todoInput = ''
    },
    toggleCheck: function(todo) {
      todo.checked = !todo.checked
    },
    destroyTodo: function(index) {
      this.todoList.pop(index);
    },
    toggleAll: function() {
      const checkedList = this.todoList.filter(todo => todo.checked);
      const uncheckedList = this.todoList.filter(todo => !todo.checked);
      if(checkedList.length != this.todoList.length){
        uncheckedList.forEach(todo => {
          todo.checked = true
        })
      }
      else {
        this.todoList.forEach(todo => {
          todo.checked = false
        })
      }
    },
    clearCompleted: function() {
      const uncheckedList = this.todoList.filter(todo => !todo.checked);
      this.todoList = uncheckedList
    },
    adjustFilter: function(filter) {
      this.filterStatus = filter
    }
  },
  computed: {
    leftItems: function() {
      return this.todoList.filter(todo => !todo.checked).length
    },
    filteredTodoList: function() {
      switch (this.filterStatus) {
        case Filter.ALL:
          return this.todoList;
        case Filter.ACTIVE:
          return this.todoList.filter(todo => !todo.checked);
        case Filter.COMPLETED:
          return this.todoList.filter(todo => todo.checked);
        default:
          return this.todoList
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
