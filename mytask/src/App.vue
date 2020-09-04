<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo"/>
    <AddTodo v-on:add-todo="addTodo"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';

@Component({
  components: {
    HelloWorld,
    Todos,
    AddTodo,
  },
})



export default class App extends Vue {

  mounted() {
    if (sessionStorage.getItem('todos')!=null) {
      try {
        const toReceive = sessionStorage.getItem('todos');
        if(toReceive!=null){
          this.todos = JSON.parse(toReceive);
        }
      } catch(e) {
        sessionStorage.removeItem('todos');
      }
    }
  }

  public addTodo(newTodo: TodoItem): void {
    const updatedTodos = [...this.todos, newTodo];
    this.todos = updatedTodos;
    const parsed = JSON.stringify(this.todos);
    sessionStorage.setItem('todos', parsed);
  }

  public deleteTodo(todoId: Number): void {
    const updatedTodos = this.todos.filter((todo: TodoItem) => todo.id !== todoId);
    this.todos = updatedTodos;
    const parsed = JSON.stringify(this.todos);
    sessionStorage.setItem('todos', parsed);
  }

  public saveToStorage():void{
    
  }

  private todos: Array<TodoItem> = [ 
  ];
}

interface TodoItem {
    id: number;
    title: string;
    completed: boolean;
  }

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
