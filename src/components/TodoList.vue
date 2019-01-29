<template>
    <div>
        <ol>
            <li 
                v-for="(todoItem, index) in list"
                :key="index"
                class="todo-item"
            >
                <input 
                    type="checkbox" 
                    :id="`check${index}`"
                    :checked="todoItem.status === 'done'"
                    @change="handleCheckboxClick(todoItem, $event)"
                >
                <label 
                    class="todo-item__name" 
                    :for="`check${index}`"
                >{{ todoItem.name }}</label>
            </li>
        </ol>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from "vue-property-decorator";
import Todo from "../models/Todo";

@Component
export default class App extends Vue {
  @Prop(Array) list!: Array<Todo>;

  @Emit("check-change")
  handleCheckboxClick(todoItem: Todo, e: Event) {
    let checked = (<HTMLInputElement>e.target).checked;
    return { status: checked ? "done" : "todo" };
  }
}
</script>


<style scoped lang="scss">
.todo-item {
  font-size: 16px;
  height: 20px;
  margin-top: 14px;
  display: flex;
  align-items: center;
}
.todo-item__name {
  margin-left: 10px;
}
</style>
