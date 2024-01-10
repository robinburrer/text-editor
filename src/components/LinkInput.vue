<script setup lang="ts">
interface Props {
  title: string
}

const props = defineProps<Props>();

</script>

<template>
  <div class="link-area">
    <label>{{ title }}</label>
    <input type="text" />
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
