<script setup lang="ts">
import { marked } from 'marked';

import { ref, onMounted } from 'vue';
import LinkInput from './LinkInput.vue';

// init stuff
const savedCursorPosition = { start: 0, end: 0 };
const textarea = ref<HTMLTextAreaElement>();
const outputArea= ref<HTMLDivElement> ();

const linkObj = ref( {
  title: 'Foo',
  url: 'https://google.com',
});

/**
 * addLink
 */
const addLink = () => {
  console.log(linkObj.value)
  const markdownLink = createMarkdownLink(linkObj.value.title, linkObj.value.url)
  insertTextAtCursor(markdownLink);
  updateOutput()
}

/**
 * insertTextAtCursor
 * @param text 
 */
function insertTextAtCursor(text: string) {
  if (textarea.value) {
    var cursorPos = textarea.value?.selectionStart;
    var textBefore = textarea.value?.value.substring(0, cursorPos);
    var textAfter = textarea.value?.value.substring(cursorPos);
 
      textarea.value.value = textBefore + text + textAfter;
      textarea.value?.setSelectionRange(cursorPos + text.length, cursorPos + text.length);
    
      textarea.value?.focus();
    }

    
    // Move the cursor position after the inserted text

  }

  const createMarkdownLink  = (title: string, url: string) => {
    return `[${title}](${url})`;
  }

  const convertMarkdownToHtml = (md: string) => {

   return marked(md)
  }

  const updateOutput = () => {
    if (outputArea.value && textarea.value) {
      console.log('md',textarea.value.value)
      console.log( convertMarkdownToHtml(textarea.value.value))
      outputArea.value.innerHTML =  convertMarkdownToHtml(textarea.value.value) as string;
    }

  }

  onMounted(updateOutput);

  




function saveCursorPosition() {
  if (!textarea.value)  return;

  savedCursorPosition.start = textarea.value.selectionStart;
  savedCursorPosition.end = textarea.value.selectionEnd;

  console.log("Cursor position saved:", savedCursorPosition);
}

  // function restoreCursorPosition() {
  //   textarea.value.focus();
  //   textarea.value.setSelectionRange(savedCursorPosition.start, savedCursorPosition.end);

  //   console.log("Cursor position restored to:", savedCursorPosition);
  // }
</script>

<template>
  <div class="editor">


    <h1>TextEditor PT</h1>

    <textarea ref="textarea" @blur="saveCursorPosition"># Headline</textarea>
    <hr>
    <div class="link-area">
      <LinkInput title="Link Name:" @blur="(event) => linkObj.title = event" :defaultValue="linkObj.title" />
      <LinkInput title="URL:" @blur="(event) => linkObj.url = event" :defaultValue="linkObj.url" />
    </div>

    <button @click="addLink">Add Link</button>

    <!-- <button @click="saveCursorPosition">Save Cursor Position</button> -->
    <!-- <button @click="restoreCursorPosition">Restore Cursor Position</button> -->


    <hr>

    <h2>Rendered Version:</h2>

    <div ref="outputArea"></div>

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
  margin-bottom: 20px;
}


textarea {
  width: 100%;
  height: 200pX;
}
</style>
