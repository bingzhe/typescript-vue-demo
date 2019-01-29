<template>
    <div>
       <input type="text" v-model="text">
       <button @click="addTodo">添加</button>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Emit } from "vue-property-decorator";

@Component
export default class App extends Vue {
    text: string = ""

    @Emit()
    addTodo(){
      return this.text;
    }
}
</script>
