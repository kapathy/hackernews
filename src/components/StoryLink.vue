<script setup>
defineProps({
  url: {
    type: String,
    required: true
  }
});
</script>

<template>
  <a :href="url" target="_blank" class="read-story">
    <slot></slot>
  </a>
</template>

<style scoped>
.read-story {
  background-color: var(--accent-color);
  color: #fff;
  padding: 10px 15px;
  border-radius: 5px;
  text-decoration: none;
  font-weight: bold;
  position: absolute;
  bottom: 15px;
  right: 15px;
}
</style>