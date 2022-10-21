<template>
    <div
    v-for="(todoList, index) in todos"
    :key="todoList.id"
    class="card mt-2">
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input
          class="form-check-input"
          type="checkbox"
          :value="todoList.completed"
          @change="toggleTodo(index)"
          >
          <label
          class="form-check-label"
          :class="{ todo: todoList.completed }"
          >
            {{todoList.subject}}
          </label>
        </div>
        <button
        class="btn btn-danger btn-sm"
        @click="delete_Todo(index)"
        >Delete</button>
      </div>
    </div>
</template>

<script>
export default {
  props: ["todos"],
  emits: [
    "toggle-todo",
    "delete-todo",
  ],
  setup(props, { emit }){
    const toggleTodo = (index) => {
      emit("toggle-todo", index)
    }
    const delete_Todo = (index) => {
      emit("delete-todo", index)
    }

    return {
      toggleTodo,
      delete_Todo,
    }
  }

}
</script>

<style>

</style>