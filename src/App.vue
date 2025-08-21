<script setup>
import { computed, ref } from 'vue';
import { marked } from 'marked';
import { debounce } from 'lodash-es';

const inputValue = ref('# hello')

const output = computed(() => {
  return marked(inputValue.value)
})

const update = debounce ((event) => {
  inputValue.value = event.target.value;
}, 100)

</script>

<template>
  <div class="editor">
    <textarea class="input" @input="update" :value="inputValue">
    </textarea>

    <div class="output" v-html="output"></div>

  </div>
</template>

<style scoped>
   body {
    margin: 0;
   }

   .editor {
    height: 100vh;
    display: flex;
    flex-direction: row;
   }

   .input, .output {
    overflow: auto;
    width: 50%;
    height: 100%;
    padding: 10px;
    font-size: 16px;
    border: none;
    box-sizing: border-box;
   }

   .input {
    background-color: #f0f0f0;
    color: #333;
   }

    .output {
      background-color: #fff;
      color: #000;
      overflow-y: auto;
    }
</style>
