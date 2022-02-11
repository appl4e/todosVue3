

<template>
  <div class="app-container">
    <h1 class="app-title">Vuejs todos</h1>
    <div class="composer">
      <input
        type="text"
        placeholder="Type and hit enter..."
        v-model="newTodo"
        class="composer__input"
        @keyup.enter="addTodo()"
      />
      <div class="filter">
        <div class="filter__left">
          <button class="filter__button filter__button--active">All ({{ allTodo }})</button>
          <button class="filter__button">Pending (0)</button>
          <button class="filter__button">Done (0)</button>
        </div>
        <div>
          <button class="filter__button filter__button--danger" @click="clearTodo()">Clear</button>
        </div>
      </div>
    </div>

    <div class="todos">
      <!-- Todo start -->
      <div
        class="todo"
        :class="{ 'todo--done': todo.done }"
        v-for="todo in todos"
        :key="todo.id"
        @click="todo.done = !todo.done"
      >
        <div class="todo__status-dot"></div>
        <div>
          <p class="todo__content">{{ todo.task }}</p>
          <small class="todo__time">{{ todo.dateTime }}</small>
        </div>
      </div>
      <!-- Todo end -->
    </div>
  </div>
</template>

<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
export default {
  data() {
    return {
      todos: [],
      newTodo: '',
    }
  },

  methods: {
    addTodo() {
      // let maxId = 0;
      // console.log(this.todos.legnth);
      // if (!this.todos.legnth) {
      //   maxId = 1;
      // }
      // else {
      //   const ids = this.todos.map(todo => todo.id);
      //   maxId = ids.reduce((a, b) => {
      //     return Math.max(a, b)
      //   });
      // }
      const newEntry = {
        id: Math.random(),
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
      console.log(this.todos.legnth);
      return this.todos.legnth;
    }
  },
}
</script>