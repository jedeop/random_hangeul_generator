<template>
  <h1>무작위 한글 생성기</h1>
  <div class="inputs">
    <div class="input-div">
      <label for="length">길이</label>
      <input type="number" name="length" id="length" v-model="state.length" placeholder="10" step="1">
    </div>

    <div class="input-div">
      <label for="jongsung">종성 없이</label>
      <input type="checkbox" name="jongsung" id="jongsung" v-model="state.removeJongsung">
      <label for="jongsung" id="jongsung_checkbox"></label>
    </div>

    <input type="button" name="generate" value="생성하기" @click="generate">
  </div>
  <div class="result">
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

<style>
   @font-face { font-family: 'RIDIBatang'; src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_twelve@1.0/RIDIBatang.woff') format('woff'); font-weight: normal; font-style: normal; } 

  * {
    font-family: 'RIDIBatang';
    font-size: 25px;
    margin: 10px;
  }
  h1 {
    font-size: 2em;
  }
  input {
    border: none;
    background-color: hsl(0, 0%, 90%);
    padding: 5px;
    border-radius: 10px;
    outline: none;
    -webkit-appearance: none;
  }
  .input-div {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  input[type="checkbox"] {
    display: none;
  }
  input[type="button"] {
    padding-left: 10px;
    padding-right: 10px;
  }
  #jongsung_checkbox {
    width: 1em;
    height: 1em;
    background-color: hsl(0, 0%, 80%);
    box-shadow: inset 0px 0 3px 0px gray;
    border-radius: 50%;
  }
  #jongsung:checked + #jongsung_checkbox {
    background-color: hsl(0, 0%, 20%);
  }
  #length {
    width: 150px;
  }
</style>