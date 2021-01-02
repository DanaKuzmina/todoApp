<template>
 <!-- eslint-disable max-len -->
  <div id="app">
    <h1 class="titile">{{ title }}</h1>
    <div class="todo">
      <input v-model="todo" type="text" placeholder="type todo..."/>
      <button @click='addTodo(id++)'>add todo</button>
      <!--<p>{{ todo }}</p>-->
      <todo-list :todos='todos' @removeTodo='removeTodo' />
      <todo-total :todos='todos' :title='titleTodoLength'/>
      <hr />
    </div>
  </div>
</template>
<script>
import todoList from './components/todoList.vue';

import todoTotal from './components/todoTotal.vue';

export default {
  components: {
    todoList,
    todoTotal,
  },
  data() {
    return {
      title: 'Todo app',
      titleTodoLength: 'Список дел',
      todo: '',
      todos: [],
      isDone: false,
      id: 0,
    };
  },
  async mounted() {
    const data = await localStorage.getItem('todos');
    if (data) {
      this.todos = JSON.parse(data);
    }
  },
  methods: {
    addTodo() {
      if (this.todo !== '') {
        this.todos.push({
          id: this.id,
          text: this.todo,
          isComplete: this.isDone,
        });
        localStorage.setItem('todos', JSON.stringify(this.todos));
      }
      this.todo = '';
    },
    removeTodo(index) {
      console.log(index);
      this.todos.splice(index, 1);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
  },
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.title {
  text-align: center;
}
.todo {
  width: 300px;
  height: 100%;
  background: rgb(156, 156, 156);
  padding: 30px;
  outline: 1px solid black;
  min-height: 500px;

  &__id {
    color: rgb(0, 0, 0);
    font-weight: bold;
  }

  &__text {
    font-size: 15px;
    color: #444;
    text-transform: capitalize;
    &__isShow {
      color: #ccc;
      text-decoration: line-through;
    }
  }

  &__check {
    display: inline-block;
    margin-left: 10px;
  }
}
</style>
