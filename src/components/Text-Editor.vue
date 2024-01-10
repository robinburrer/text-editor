<script setup lang="ts">
import { ref } from 'vue';
import LinkInput from './LinkInput.vue';


const linkObj = ref( {
  title: '',
  url: '',
});

const addLink = () => {
  console.log(linkObj.value)
}

const textarea = ref();


var savedCursorPosition = { start: 0, end: 0 };

function saveCursorPosition() {
    savedCursorPosition.start = textarea.value.selectionStart;
    savedCursorPosition.end = textarea.value.selectionEnd;

    console.log("Cursor position saved:", savedCursorPosition);
  }

  function restoreCursorPosition() {
    textarea.value.focus();
    textarea.value.setSelectionRange(savedCursorPosition.start, savedCursorPosition.end);

    console.log("Cursor position restored to:", savedCursorPosition);
  }
</script>

<template>
  <div class="editor">


  <h1>TextEditor PT</h1>

  <textarea ref="textarea"> </textarea>
  <hr>
  <div class="link-area">
    <LinkInput title="Link Name:" @blur="(event) => linkObj.title = event" />
    <LinkInput title="URL:" @blur="(event) => linkObj.url = event"/>
  </div>

  <button @click="addLink">Add Link</button>

    <button @click="saveCursorPosition">Save Cursor Position</button>
  <button @click="restoreCursorPosition">Restore Cursor Position</button>

</div>
</template>

<style scoped>

  h1 {
    margin-bottom: 10px;
    width: 100%;
    text-align: center;
  }


  button {
    width: 100%;
  }


  textarea {
    width: 100%;
    height: 200pX;
  }


</style>
