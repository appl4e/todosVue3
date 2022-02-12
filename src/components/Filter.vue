<template>
  <div class="filter">
    <div class="filter__left">
      <button
        class="filter__button filter__button--active"
        @click="$emit('update:modelValue', 'all')"
      >All ({{ allCount }})</button>
      <button
        class="filter__button"
        @click="$emit('update:modelValue', 'pending')"
      >Pending ({{ pendingCount }})</button>
      <button
        class="filter__button"
        @click="$emit('update:modelValue', 'done')"
      >Done ({{ doneCount }})</button>
    </div>
    <div>
      <button class="filter__button filter__button--danger" @click="$emit('onClear')">Clear</button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    modelValue: {
      type: String,
      required: true
    },
    allCount: '',
    pendingCount: '',
    doneCount: ''
  }
}
</script>