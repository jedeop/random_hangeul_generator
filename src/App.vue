<template>
<div>
  <div>
    <label for="length">길이</label>
    <input type="number" name="length" id="length" v-model="state.length">
  </div>

  <div>
    <label for="jongsung">종성 없이</label>
    <input type="checkbox" name="jongsung" id="jongsung" v-model="state.removeJongsung">
  </div>

  <input type="button" name="generate" value="생성하기" @click="generate">
</div>
<div>
  {{ state.result }}
</div>
</template>

<script>
import { reactive } from 'vue';

export default {
  name: 'App',

  setup() {
    const state = reactive({
      length: 10,
      removeJongsung: false,
      result: ''
    })

    function generate() {
      let text = '';
      for (let i = 0; i < state.length; i++) {
        let code = Math.floor(Math.random() * (0xD7A3 - 0xAC00)) + 0xAC00;
        if (state.removeJongsung) {
          let lastChar = (code - 0xAC00) % (21 * 28) % 28;
          code = code - lastChar;
        }
        text += String.fromCharCode(code);
      }
      state.result = text
    }

    return {
      state,
      generate
    }
  }
}
</script>
