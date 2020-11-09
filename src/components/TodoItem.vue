<template>
  <li class="my-2 mt-4 text-lg w-8/12 sm:w-9/12">
    <div class="relative">
      <div class="inline-flex items-center cursor-pointer">
        <input
          class="transform scale-150"
          type="checkbox"
          :checked="todoItem.isChecked"
          @click="toggleTodo(todoItem.desc)"
        />
        <span
          @click="toggleTodo(todoItem.desc)"
          class="mx-3 description  font-semibold
              todoItem.isChecked "
          :class="{ 'line-through': todoItem.isChecked }"
        >
          {{ todoItem.desc }}
        </span>
        <div
          class="absolute cursor-pointer right-0 top-0 bg-gray-400 flex justify-center  items-center rounded-full w-6 h-6 hover:bg-gray-600 hover:text-gray-200 transition duration-200 ease-in-out"
          v-if="todoItem.isChecked && todoType === 'completed'"
          @click="deleteTodo(todoItem.desc)"
        >
          &times;
        </div>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  emits: ["toggletodo", "deletetodo"],
  props: {
    todoItem: {
      type: Object,
      required: true,
    },
    todoType: {
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

    return { toggleTodo, deleteTodo };
  },
};
</script>

// emits property in script written to remove the warning.

<style></style>
