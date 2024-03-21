<script lang="ts" setup>
type Step = {
  title: string;
  closeHandler: () => void;
};
defineProps<Step>();
</script>
<template>
  <div class="w3-large">
    <!-- Header -->
    <header class="brown-80-bg header">
      <span>{{ title }}</span>
      <a @click="closeHandler">
        <font-awesome-icon icon="fa-solid fa-times close" />
      </a>
    </header>

    <!-- Body -->
    <div class="w3-padding-16 w3-container">
      <slot name="body" />
    </div>

    <!-- Footer -->
    <footer class="brown-80-bg footer">
      <slot name="footer" />
    </footer>
  </div>
</template>
<style lang="scss">
.header {
  align-items: center;
  display: flex;
  justify-content: space-between;
  padding: 16px;
  a {
    cursor: pointer;
    svg {
      vertical-align: middle;
      width: 18px;
    }
  }
}

.footer {
  display: flex;
  gap: 1em;
  padding: 16px;
}
</style>
