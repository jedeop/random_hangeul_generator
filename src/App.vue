<template>
  <h1>무작위 한글 생성기</h1>
  <div class="inputs">
    <InputNumber id="length" label="길이" placeholder="10" @input-val="val => state.length = val" :value="state.length" />
    <InputCheckbox id="_jongsung" label="종성 없이 생성" @input-val="val => state.removeJongsung = val" :value="state.removeJongsung" />

    <input type="button" value="생성하기" @click="generate">
  </div>
  <div v-show="state.result">
    <div class="hr"></div>
    <input type="button" value="복사하기" :data-clipboard-text="state.result" id="copy-btn">
    <div id="result">
      {{ state.result }}
    </div>
  </div>
</template>

<script>
  import { reactive } from 'vue';
  import InputNumber from './components/InputNumber.vue'
  import InputCheckbox from './components/InputCheckbox.vue'

  export default {
    name: 'App',
    components: {
      InputNumber,
      InputCheckbox
    },
    mounted() {
      new ClipboardJS('#copy-btn')
    },
    setup() {
      const state = reactive({
        length: 10,
        removeJongsung: false,
        result: null
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

  input[type="button"] {
    padding-left: 10px;
    padding-right: 10px;
  }
  input[type="button"]:active {
    background-color: hsl(0, 0%, 80%);
  }

  #result {
    display: inline-block;
    padding: 10px;
    background-color: hsl(0, 0%, 95%);
    color: gray;
  }
  #copy-btn {
    display: block;
    margin: 10px auto;
  }
  .hr {
    margin: 30px auto;
    border-bottom: 2px hsl(0, 0%, 70%) dashed;
    width: 30%;
  }
</style>