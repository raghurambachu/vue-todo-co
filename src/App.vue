<template>
  <div
    class="min-h-screen relative bg-gray-200 text-gray-600 transition duration-200 ease-in-out"
    :class="{ 'bg-gray-900': state.mode === 'dark' }"
  >
    <Crescent
      v-if="state.mode === 'light'"
      class="absolute right-0 top-0 m-4 cursor-pointer"
      @click="setMode('dark')"
    />
    <Sun
      v-else
      class="absolute right-0 top-0 m-4 cursor-pointer"
      @click="setMode('light')"
    />
    <h1 class="font-bold text-4xl text-center pt-12 mb-8">#todo</h1>
    <div class="max-w-xl  mx-auto px-1 sm:px-0">
      <TodoType
        v-bind:activeTab="state.activeTab"
        @change-tab="changeActiveTab"
      />
      <hr className="border-b-0 border-gray-400 border-t-2" />
      <TodoInput v-bind:todos="state.todos" @addtodo="addTodo" />
      <TodoList
        v-bind:activeTab="state.activeTab"
        @toggletodo="toggleTodo"
        @deletetodo="deleteTodo"
        @deleteallcompleted="deleteAllCompleted"
        v-bind:todos="sendTodosBasedOnActiveTab(state.activeTab)"
      />
    </div>

    <div
      class="absolute bottom-0 left-0 w-56 h-56  sm:w-64 sm:h-64 bg-blue-200 rounded-t-full rounded-b-none rounded-l-none rounded-r-full md:block bottom-design bottom-circle "
    >
      <div
        :class="{ 'bg-gray-900': state.mode === 'dark' }"
        class="absolute bottom-0 left-0 w-48 h-48 sm:w-56 sm:h-56 bg-gray-200 rounded-t-full rounded-b-none rounded-l-none rounded-r-full transition duration-200 ease-in-out"
      ></div>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";

import TodoType from "./components/TodoType";
import TodoInput from "./components/TodoInput";
import TodoList from "./components/TodoList";
import Crescent from "./assets/Crescent";
import Sun from "./assets/Sun";

export default {
  name: "App",
  components: { TodoType, TodoInput, TodoList, Crescent, Sun },
  setup() {
    const state = reactive({ activeTab: "all", todos: [], mode: "light" });
    function changeActiveTab(activeTab) {
      state.activeTab = activeTab;
    }

    function sendTodosBasedOnActiveTab() {
      switch (state.activeTab) {
        case "all":
          return state.todos.slice();
        case "active":
          return state.todos.filter((todoItem) => !todoItem.isChecked);
        case "completed":
          return state.todos.filter((todoItem) => todoItem.isChecked);
        default:
          return state.todos.slice();
      }
    }

    function addTodo(todo) {
      state.todos.push(todo);
    }

    function toggleTodo(desc) {
      state.todos = state.todos.map((todoItem) => {
        if (todoItem.desc === desc) {
          return { ...todoItem, isChecked: !todoItem.isChecked };
        }
        return todoItem;
      });
    }

    function deleteTodo(desc) {
      state.todos = state.todos.filter((todoItem) => todoItem.desc !== desc);
    }

    function deleteAllCompleted() {
      state.todos = state.todos.filter((todoItem) => !todoItem.isChecked);
    }

    function setMode(mode) {
      state.mode = mode;
    }

    return {
      state,
      changeActiveTab,
      addTodo,
      sendTodosBasedOnActiveTab,
      toggleTodo,
      deleteTodo,
      deleteAllCompleted,
      setMode,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
