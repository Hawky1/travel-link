<template>
  <div id="app" >
    <nav> 
      <ul class="no-b">
        <li>
          <router-link to="main.html">HOME</router-link>
        </li>
        <li>
          <router-link to="main.html">s92067878</router-link>
        </li>
      </ul>
    </nav>
    
    <div class="container grid-xs py-2" >
      <h1 class="title">Travel To-Do here</h1>
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="Type here..." />
          <button class="btn btn-primary input-group-btn">Add</button>
        </div>
      </form>
      <div class="todo-list">
        <todo v-for="t in todos" @toggle="toggleTodo" @remove="removeTodo" :key="t.id" :todo="t"></todo>
      </div>
    </div>
  </div>
  
</template>

<script>
import Todo from "./components/Todo";

export default {
  name: "App",
  components: { Todo },
  data() {
    return { todos: [], todo: { checked: false } };
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false };
    },

    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1){
        const checked = !this.todos[index].checked
        this.$set(this.todos, index, {...this.todos[index], checked})
      }
    },

    removeTodo(todo){
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1){
        this.$delete(this.todos, index)
      }
    }
  }
};
</script>

<style scoped>

ul.no-b {
  list-style-type: none;
}

.title {
  text-align: center;
  margin: 0px 0px 20px 0px;
}

.todo-list {
  padding-top: 2rem;
}
</style>