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
  gap: 20px;
  margin: 10px 0;
}
</style>
