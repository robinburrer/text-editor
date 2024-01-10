<script setup lang="ts">
import LinkInput from './LinkInput.vue';

const addLink = () => {
  console.log('add link')
}
</script>

<template>
  <div class="editor">


  <h1>texteditor PT</h1>

  <textarea> </textarea>
  <hr>
  <div class="link-area">
    <LinkInput title="Link Name:" />
    <LinkInput title="URL:" />
  </div>

  <button @click="addLink">Add Link</button>
</div>
</template>

<style scoped>

  h1 {
    margin-bottom: 20px;
    width: 100%;
    text-align: center;
  }
  .editor {
    width: 300px;
    /* background-color: red; */
  }


  textarea {
    width: 300px;
    height: 200pX;
  }


</style>
