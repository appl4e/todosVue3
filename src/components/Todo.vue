<template>
  <!-- Todo start -->
  <div class="todo" :class="{ 'todo--done': todo.done }" @click="todo.done = !todo.done">
    <div class="todo__status-dot"></div>
    <div>
      <p class="todo__content">{{ todo.task }}</p>
      <small class="todo__time">{{ todo.dateTime }}</small>
    </div>
  </div>
  <!-- Todo end -->
</template>
<script>
export default {
  props: ["todo"]
}
</script>