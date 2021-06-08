<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <div class="inner">
      <NewTodo @addTodo="addTodo" ></NewTodo>
      <TodoList :list="list" @updateStatus="updateStatus"></TodoList>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator';
import NewTodo from './components/NewTodo.vue';
import TodoList from './components/TodoList.vue';
import Todo from './models/Todo';

@Component({
  components: {
    NewTodo,
    TodoList
  }
})
export default class App extends Vue {
  list: Array<Todo> = localStorage.getItem('todolist') ? JSON.parse(<string>localStorage.getItem('todolist')) : []  //这里用了断言，断言它肯定会返回字符串的

  @Watch('list', {deep: true})
  onListChanged(newValue: Array<Todo>){
    let list = JSON.stringify(newValue)
    localStorage.setItem('todolist', list)
  }
  
  addTodo(name: String){
    let newTodo: Todo = {name, status: 'todo'}
    this.list.push(newTodo)
  }
  updateStatus(item: Todo, part: Partial<Todo>){
    // let index = this.list.indexOf(item)
    // let newTodo = Object.assign({}, item, part)
    // this.list.splice(index, 1, newTodo)
    Object.assign(item, part)
  }
}
</script>

<style lang="scss">
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  & > .inner{
    padding: 30px;
    border: 1px solid gray;
  }
}
</style>
<style lang="css">
*{
  margin: 0; padding: 0;
  box-sizing: border-box;
}
  ol,ul{
    list-style: none;
  }
</style>
