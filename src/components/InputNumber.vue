<template>
  <div class="input-div">
    <label :for="id">{{ label }}</label>
    <input type="number" :id="id" :placeholder="placeholder" :value="value" @input="updateValue">
  </div>
</template>

<script>
  import { reactive } from 'vue'

  export default {
    name: 'InputNumber',
    props: {
      id: String,
      label: String,
      placeholder: String,
      value: Number
    },
    setup(props, context) {
      function updateValue(ev) {
        const parse = parseInt(ev.target.value)
        context.emit('input-val', parse)
      }

      return {
        updateValue
      }
    }
  }
</script>

<style>
  input[type="number"] {
    width: 150px;
  }
</style>
