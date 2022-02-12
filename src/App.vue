

<template>
  <div class="app-container">
    <h1 class="app-title">Vuejs todos</h1>
    <div class="composer">
      <AddTodo @onSubmit="addTodo()" v-model="newTodo" />
      <div class="filter">
        <div class="filter__left">
          <button
            class="filter__button filter__button--active"
            @click="filterBy = 'all'"
          >All ({{ allTodo }})</button>
          <button class="filter__button" @click="filterBy = 'pending'">Pending ({{ pending }})</button>
          <button class="filter__button" @click="filterBy = 'done'">Done ({{ done }})</button>
        </div>
        <div>
          <button class="filter__button filter__button--danger" @click="clearTodo">Clear</button>
        </div>
      </div>
    </div>

    <div class="todos">
      <Todo v-for="todo in filteredTodos" :todo="todo" :key="todo.id" />
    </div>
  </div>
</template>

<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Todo from "./components/Todo.vue"
import AddTodo from "./components/AddTodo.vue"
export default {
  components: {
    Todo,
    AddTodo
  },
  data() {
    return {
      todos: [],
      newTodo: '',
      filterBy: 'all'
    }
  },

  methods: {
    addTodo(e) {
      let maxId = 0;
      console.log(this.todos.length);
      if (this.todos.length == 0) {
        maxId = 0;
      }
      else {
        const ids = this.todos.map(todo => todo.id);
        maxId = ids.reduce((a, b) => {
          return Math.max(a, b)
        });
      }
      const newEntry = {
        id: maxId + 1,
        task: this.newTodo,
        dateTime: new Date().toString(),
        done: false
      }

      this.todos.unshift(newEntry);
      this.newTodo = "";
    },
    clearTodo() {
      this.todos = this.todos.filter((todo) => todo.done == false);
      if (this.todos.legnth == 0) {
        this.todos = [{
          id: '', task: '',
          dateTime: '',
          done: false
        }
        ]
      }
    }
  },
  computed: {
    allTodo() {
      return this.todos.length;
    },
    pending() {
      return this.todos.filter((todo) => !todo.done).length
    },
    done() {
      return this.todos.filter((todo) => todo.done).length
    },
    filteredTodos() {
      if (this.filterBy == 'all') {
        return this.todos;
      }
      if (this.filterBy == 'pending') {
        return this.todos.filter((todo) => !todo.done);
      }
      if (this.filterBy == 'done') {
        return this.todos.filter((todo) => todo.done);
      }
    }
  },
}
</script>