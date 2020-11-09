<template>
  <div
    class="todo-type text-sm sm:text-base flex justify-evenly space-x-2 xs:space-x-6 sm:space-x-12 "
  >
    <div class="relative py-1">
      <button
        class="btn-all font-bold focus:outline-none pb-1 w-24"
        @click="handleTabClick('all')"
      >
        All
      </button>
      <span
        v-if="activeTab === 'all'"
        class="absolute bottom-0 left-0  border-blue-500 inline-block rounded-t  border-b-4 w-24 transition duration-200 ease-in-out"
      ></span>
    </div>
    <div class="relative">
      <button
        class="btn-all font-bold focus:outline-none pb-1 w-24"
        @click="handleTabClick('active')"
      >
        Active
      </button>
      <span
        v-if="activeTab === 'active'"
        class="absolute bottom-0 left-0 border-blue-500 inline-block rounded-t  border-b-4 w-24 transition duration-200 ease-in-out"
      ></span>
    </div>
    <div class="relative">
      <button
        class="btn-all font-bold focus:outline-none pb-1 w-24 "
        @click="handleTabClick('completed')"
      >
        Completed
      </button>
      <span
        v-if="activeTab === 'completed'"
        class="absolute bottom-0 left-0 border-blue-500 inline-block rounded-t  border-b-4 w-24 transition duration-200 ease-in-out"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoType",
  props: {
    activeTab: {
      type: String,
      required: true,
    },
  },
  setup(props, ctx) {
    function handleTabClick(activeTab) {
      ctx.emit("change-tab", activeTab);
    }

    return {
      handleTabClick,
    };
  },
};
</script>

<style></style>
