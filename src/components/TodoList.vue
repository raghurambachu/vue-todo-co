<template>
  <ul className="px-1">
    <TodoItem
      v-for="todoItem in todos"
      :key="todoItem.id"
      :todoItem="todoItem"
      @toggletodo="toggleTodo"
      @deletetodo="deleteTodo"
      :todoType="activeTab"
    />
  </ul>
  <div
    class="flex justify-center"
    title="Delete completed"
    @click="deleteAllCompletedTodos"
    v-if="todos.length && activeTab === 'completed'"
  >
    <button
      class="text-blue-100 w-12 h-12 mt-16 bg-gray-300 text-red-100 text-2xl rounded-full hover:bg-gray-500 rounded-sm shadow-md text-sm font-semibold focus:outline-none"
    >
      🗑️
    </button>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "TodoList",
  emits: ["deletetodo", "toggletodo", "deleteallcompleted"],
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
      required: true,
    },
    activeTab: {
      type: String,
      required: true,
    },
  },
  setup(props, ctx) {
    function toggleTodo(desc) {
      ctx.emit("toggletodo", desc);
    }

    function deleteTodo(desc) {
      ctx.emit("deletetodo", desc);
    }

    function deleteAllCompletedTodos() {
      ctx.emit("deleteallcompleted");
      //   can write kebab case, but doing so there was a warning, so had to write as one string.
    }

    return { toggleTodo, deleteTodo, deleteAllCompletedTodos };
  },
};
</script>

<style></style>
