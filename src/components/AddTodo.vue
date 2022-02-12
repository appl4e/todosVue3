<template>
  <form @submit.prevent="$emit('onSubmit')">
    <input
      type="text"
      placeholder="Type and hit enter..."
      :value="modelValue"
      @keydown="$emit('update:modelValue', $event.target.value)"
      class="composer__input"
    />
  </form>
</template>
<script>
export default {
  props: {
    modelValue: {
      type: String,
      required: true
    }
  },

}
</script>