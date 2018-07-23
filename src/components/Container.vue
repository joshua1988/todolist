<template>
  <div>
    <todo-list
      v-bind:todoList="todoList"
      v-bind:filteredTodoList="filteredTodoList"
      v-on:toggleCheck="toggleCheck"
      v-on:destroyTodo="destroyTodo"
      v-on:toggleAll="toggleAll"
    />
    <!-- This footer should hidden by default and shown when there are todos -->
    <footer class="footer">
      <!-- This should be `0 items left` by default -->
      <span class="todo-count">
        <strong>{{ leftItems }}</strong> item left</span>
      <!-- Remove this if you don't implement routing -->
      <ul class="filters">
        <li>
          <a class="selected" href="#/">All</a>
        </li>
        <li>
          <a href="#/active" v-on:click="filterActive">Active</a>
        </li>
        <li>
          <a href="#/completed">Completed</a>
        </li>
      </ul>
      <!-- Hidden if no completed items are left ↓ -->
      <button class="clear-completed" v-on:click="clearCompleted">Clear completed</button>
    </footer>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  name: 'Container',
  components: {
    'todo-list': TodoList
  },
  props: {
    todoList: Array,
    filteredTodoList: Array,
    filterStatus: String
  },
  methods: {
    toggleCheck: function(todo) {
      this.$emit('toggleCheck', todo)
    },
    destroyTodo: function(index) {
      this.$emit('destroyTodo', index)
    },
    toggleAll: function() {
      this.$emit('toggleAll')
    },
    clearCompleted: function() {
      this.$emit('clearCompleted')
    },
    filterActive: function() {
      this.$emit('filterActive')
    }
  },
  computed: {
    leftItems: function() {
      return this.todoList.filter(todo => !todo.checked).length
    }
  }
}
</script>

<style scoped>

</style>
