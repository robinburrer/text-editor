<script setup lang="ts">
import { ref } from 'vue';
import LinkInput from './LinkInput.vue';

// init stuff
const savedCursorPosition = { start: 0, end: 0 };
const textarea = ref();

const linkObj = ref( {
  title: '',
  url: '',
});

/**
 * addLink
 */
const addLink = () => {
  console.log(linkObj.value)
  const markdownLink = createMarkdownLink(linkObj.value.title, linkObj.value.url)
  insertTextAtCursor(markdownLink)
}

/**
 * insertTextAtCursor
 * @param text 
 */
function insertTextAtCursor(text: string) {
   
    var cursorPos = textarea.value.selectionStart;
    var textBefore = textarea.value.value.substring(0, cursorPos);
    var textAfter = textarea.value.value.substring(cursorPos);
    textarea.value.value = textBefore + text + textAfter;
    
    // Move the cursor position after the inserted text
    textarea.value.setSelectionRange(cursorPos + text.length, cursorPos + text.length);
    
    textarea.value.focus();
  }

  const createMarkdownLink  = (title: string, url: string) => {
    return `[${title}](${url})`;
  }






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
