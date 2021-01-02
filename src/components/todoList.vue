<template>
<!-- eslint-disable max-len -->
  <div>
    <div v-for="(todo, i) in todos" :key="todo.id">
      <p>
        <span class="todo__id">{{ i + 1 }}. </span>
        <span @dblclick='removeItem(i)' class="todo__text" :class="{todo__text__isShow: todo.isComplete}">
          {{ todo.text }}
        </span>
      <input v-model="todo.isComplete" class="todo__check" type="checkbox" />
      </p>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    todos: {
      type: [Array],
      requared: true,
    },
    removeTodo: {
      type: Function,
    },
  },
  methods: {
    removeItem(index) {
      this.$emit('removeTodo', index);
    },
  },
};
</script>
