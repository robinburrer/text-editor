<script setup lang="ts">
import { ref } from 'vue'
interface Props {
  title: string
}

const props = defineProps<Props>();
const emit = defineEmits(['blur'])

const textValue = ref('');
  

const blurHandler = () => {
  console.log('blur', textValue.value);

  emit('blur',textValue.value);
}

</script>

<template>
  <div class="link-area">
    <label>{{ title }}</label>
    <input type="text" @blur="blurHandler" v-model="textValue"/>
  </div>
</template>

<style scoped>  

label {
  min-width: 80px;
}
.link-area {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  text-align: left;


  margin: 10px 0;
  width: 100%;

}
</style>
