<template>
  <div class="input-div">
    <label :for="id">{{ label }}</label>
    <input type="checkbox" :id="id" @change="updateValue" :checked="value">
    <label :for="id" class="checkbox-real"></label>
  </div>
</template>

<script>
  import { reactive } from 'vue'

  export default {
    name: 'InputCheckbox',
    props: {
      id: String,
      label: String,
      value: Boolean
    },
    setup(props, context) {
      function updateValue(ev) {
        context.emit('input-val', ev.target.checked)
      }

      return {
        updateValue
      }
    }
  }
</script>

<style>
  input[type="checkbox"] {
    display: none;
  }
  .checkbox-real {
    width: 1em;
    height: 1em;
    background-color: hsl(0, 0%, 80%);
    box-shadow: inset 0px 0 3px 0px gray;
    border-radius: 50%;
  }
  input[type="checkbox"]:checked + .checkbox-real {
    background-color: hsl(0, 0%, 20%);
  }
</style>
