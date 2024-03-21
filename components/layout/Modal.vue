<script lang="ts" setup>
defineProps(["show"]);
</script>
<template>
  <div class="w3-modal" :class="{ 'd-block': show, 'd-none': !show }">
    <div class="w3-modal-content w3-animate-top w3-round-large hidden-overflow">
      <slot />
    </div>
  </div>
</template>
<style>
.d-block {
  display: block;
}
.d-none {
  display: none;
}
.hidden-overflow {
  overflow: hidden;
}
</style>
