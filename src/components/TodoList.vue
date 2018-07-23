<template>
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox" v-on:click="toggleAll">
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list" v-for="(todo, index) in filteredTodoList" :key="index">
      <!-- These are here just to show the structure of the list items -->
      <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
      <li v-bind:class="{completed : todo.checked}">
        <div class="view">
          <input class="toggle" type="checkbox" :checked="todo.checked ? true : false" v-on:click="toggleCheck(todo)">
          <label>{{ todo.title }}</label>
          <button class="destroy" v-on:click="destroyTodo(index)"></button>
        </div>
        <input class="edit" value="Create a TodoMVC template">
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    filteredTodoList: Array
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
    }
  }
}
</script>

<style>

</style>
