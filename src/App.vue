<template>
  <div id="app">
    <div class="inner">
      <new-todo 
        @add-todo="addTodo"        
      />
      <todo-list 
        :list="list"
        @check-change="updateTodo"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";

import NewTodo from "./components/NewTodo.vue";
import TodoList from "./components/TodoList.vue";
import Todo from "./models/Todo";

@Component({
  components: {
    NewTodo,
    TodoList
  }
})
export default class App extends Vue {
  list: Array<Todo> = localStorage.getItem("data")
    ? JSON.parse(<string>localStorage.getItem("data"))
    : [];

  @Watch("list")
  onWatchChagne(value: Array<Todo>) {
    let string = JSON.stringify(value);
    localStorage.setItem("data", string);
  }

  addTodo(name: string) {
    let todo: Todo = { name: name, status: "todo" };
    this.list.push(todo);
  }

  updateTodo(part: Partial<Todo>, todo: Todo) {
    let index: number = this.list.indexOf(todo);
    let newTodo: Todo = Object.assign({}, todo, part);

    this.list.splice(index, 1, newTodo);
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  justify-content: center;
  align-items: center;

  .inner {
    border: 1px solid #ccc;
    padding: 30px;
  }
}
* {
  margin: 0;
  padding: 0;
}
ul,
ol {
  list-style: none;
}
</style>