<template>
    <form
    @submit.prevent="onSubmit"
    >
    <div class="d-flex">
      <div class="flex-grow-1 mr-2">
        <input
        class="form-control"
        type="text"
        v-model="todo"
        placeholder="Type new to-do"
        >
      </div>
      <div>
        <button
        class="btn btn-primary"
        type = "submit"
        >
        add
        </button>
      </div>
    </div>
    <!-- 자주 바뀌는 곳은 v-show, 자주 안바뀌는 곳은 v-if -->
    <div
    v-show="hasError"
    style="color: red"
    >This field connot be empty</div>
    </form>
</template>

<script>
import { ref } from '@vue/reactivity';
export default {
    
    emits: [
        "add-todo",
    ],

    setup(props, {emit}){
        const todo = ref("");
        const hasError = ref(false);

        const onSubmit = () => {
            if(todo.value === ""){
                hasError.value = true;
            } else {
                emit("add-todo", {
                    id: Date.now(),
                    subject: todo.value,
                    completed: false,
                })
                hasError.value = false;
                todo.value = "";
            }
        }

        return {
            todo,
            hasError,
            onSubmit,
        }
    }
}
</script>

<style>
</style>