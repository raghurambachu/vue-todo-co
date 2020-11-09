<template>
  <form class="flex justify-between mt-6" @submit.prevent="handleSubmit">
    <div class="w-8/12 sm:w-9/12">
      <input
        type="text"
        id="desc"
        name="desc"
        v-model="state.desc"
        placeholder="add details"
        class="p-2 sm:py-3 border text-sm  sm:text-base border-gray-500 w-full rounded-md block bg-gray-100 focus:outline-none "
      />
    </div>
    <button
      type="submit"
      class="w-3/12 sm:w-2/12 bg-blue-600 shadow-md font-semibold text-blue-100 rounded-md self-start py-2 text-sm  sm:text-base sm:py-3 hover:bg-blue-500 transition duration-200 ease-in-out "
    >
      Add
    </button>
  </form>
  <small class="text-red-500 mb-4" v-if="state.error">{{ state.error }}</small>
</template>

<script>
import { reactive } from "vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "TodoInput",
  emits: ["addtodo"],
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  setup(props, ctx) {
    const state = reactive({
      desc: "",
      error: "",
    });

    function handleSubmit() {
      state.error = "";
      if (state.desc === "") {
        state.error = "Todo cannot be empty";
      } else if (props.todos.some((todo) => todo.desc === state.desc)) {
        state.error = "Todo already exists, cannot be added";
        state.desc = "";
      } else {
        const todo = { id: uuidv4(), desc: state.desc, isChecked: false };
        ctx.emit("addtodo", todo);
        state.desc = "";
      }
    }
    return { state, handleSubmit };
  },
};
</script>

<style></style>
