<template>
  <div>
    <h2 contenteditable="true" @mouseleave="changeText($event)">{{ title }}</h2>
    <ul>
      <li v-bind:key="todo.id" v-for="todo in todos">
        <Todo v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)"/>
      </li>
    </ul>


    <!-- <ul class="todo-list">
        <li @dragover.prevent @drop="dragFinish(-1, $event)" v-if="dragging > -1" class="trash-drop todo-item" v-bind:class="{drag: isDragging}">Delete</li>
        
        <li v-else>
        <input placeholder="Type new task and press enter" type="text" class="new-todo todo-item" v-model="newItem" @keyup.enter="addItem">
        </li>
        
        <li class="todo-item" v-for="(item, i) in todos" v-key="i" draggable="true" @dragstart="dragStart(i, $event)" @dragover.prevent @dragenter="dragEnter" @dragleave="dragLeave" @dragend="dragEnd" @drop="dragFinish(i, $event)">
        <input type="checkbox" v-model="item.done" />
        <span :class="{done: item.done}">{{ item.title }}</span>
        <span class="remove-item" @click="removeItem(item)">x</span>
        </li>
    </ul> -->


  </div>
</template>
<script>
import Todo from './Todo';
export default {
  name: 'Todos',
  data() {
    return {
      title: 'New TODO List'
    }
  },
  methods: {
      changeText(e){
          e.target.blur();
          this.title = e.target.innerText;
          sessionStorage.setItem('nameOfList', this.title);
      }
  },
  mounted(){
      const receivedName = sessionStorage.getItem('nameOfList');
      if (receivedName!=null){
          this.title = receivedName;
      }
  },
  components: {
    Todo
  },
  props: [
      "todos",
  ]
}
</script>
<style scoped>
</style>