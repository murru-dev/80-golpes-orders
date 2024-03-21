<script lang="ts" setup>
defineProps(["title"]);
</script>
<template>
  <div class="w3-container w3-padding-64 w3-xxlarge">
    <div class="w3-content section-container">
      <!-- Title -->
      <h1 class="w3-center white-80-text capitals title">
        {{ title }}
      </h1>
      <!-- Body -->
      <slot />
    </div>
  </div>
</template>
<style>
.title {
  margin-bottom: 64px;
}
.section-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
