<template>
  <div v-bind:class="{ 'completed': todo.completed }">
    <p contenteditable="true" @mouseleave="changeText($event)">{{ todo.title }}</p>
    <button v-on:click="markComplete">Done</button>
    <button @click="$emit('delete-todo', todo.id)">Delete</button>
  </div>
</template>
<script>
export default {
  name: 'Todo',
  props: [
    "todo"
  ],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      const toReplace = this.todo;
      const todoList = JSON.parse(sessionStorage.getItem('todos'));
      const updatedTodos = todoList.filter((todo) => todo.id !== this.todo.id);
      const newUpdatedTodos = [...updatedTodos, toReplace];
      sessionStorage.setItem('todos', JSON.stringify(newUpdatedTodos));
    },
    onInput(e) {
        this.todo.title = e.target.innerText;
        const toReplace = this.todo;
        const todoList = JSON.parse(sessionStorage.getItem('todos'));
        const updatedTodos = todoList.filter((todo) => todo.id !== this.todo.id);
        const newUpdatedTodos = [...updatedTodos, toReplace];
        sessionStorage.setItem('todos', JSON.stringify(newUpdatedTodos));
    },
    changeText(e) {
        e.target.blur();
        this.todo.title = e.target.innerText;
        const toReplace = this.todo;
        const todoList = JSON.parse(sessionStorage.getItem('todos'));
        const updatedTodos = todoList.filter((todo) => todo.id !== this.todo.id);
        const newUpdatedTodos = [...updatedTodos, toReplace];
        sessionStorage.setItem('todos', JSON.stringify(newUpdatedTodos));
    },
  }
}
</script>
<style scoped>
  .completed {
    text-decoration: line-through;
  }
</style>