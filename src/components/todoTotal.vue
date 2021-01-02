<template>
    <div>
        <p>{{title}} {{todos.length}}</p>
    </div>
</template>
<script>
export default {
  props: {
    title: {
      type: [String],
      requared: true,
    },
    todos: {
      type: [Array],
      requared: true,
    },
  },
};
</script>
