<!--  v-on:  === @      ///     v-bind: === : -->

<template>
  <div class="container">
    <h2>To-Do List</h2>
    <input
    class="form-control"
    type="text"
    v-model="searchText"
    placeholder="Search"
    >
    <hr />
    <TodoSimpleForm
    @add-todo="addTodo"
     />

    <div v-if="!filteredTodos.length">
      there is nothing to display
    </div>

    <TodoList
    :todos="filteredTodos"
    @toggle-todo="toggleTodo"
    @delete-todo="delete_Todo"
    />

  </div>
</template>

<script>
import { ref, computed } from '@vue/reactivity';
import TodoSimpleForm from "./components/TodoSimpleForm.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoSimpleForm,
    TodoList,
  },

  setup(){
    const todos = ref([]);
    const searchText = ref("");

    const todoStyle = {
      textDecoration: "line-through",
      color: "gray"
    }

    const addTodo = (todo) => {
      todos.value.push(todo)
    }
    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    }
    const delete_Todo = (index) => {
      todos.value.splice(index, 1)
    }

    const filteredTodos = computed(() => {
      if(searchText.value){
        return todos.value.filter(todo => {
          return todo.subject.includes(searchText.value)
        })
      }
      return todos.value;
    })



    return {
      todos,
      addTodo,
      todoStyle,
      delete_Todo,
      toggleTodo,
      searchText,
      filteredTodos,
    }
  }
}


</script>

<style>
.todo {
  color: gray;
  text-decoration: line-through;
}
</style>