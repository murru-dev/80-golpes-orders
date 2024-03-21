<script lang="ts" setup>
const emits = defineEmits(["cancelOrder"]);
const handleCloseOrder = () => {
  emits("cancelOrder");
  renderedComponent.value = "OrderAuth";
};
/* Steps components */
const auth = resolveComponent("OrderAuth");
const register = resolveComponent("OrderRegister");
const payMethod = resolveComponent("OrderPayMethod");
const renderedComponent = ref<string>("OrderAuth");
provide("change-step", (component: string) => {
  renderedComponent.value = component;
});
let step = computed(() => {
  switch (renderedComponent.value) {
    case "OrderRegister":
      return register;
    case "OrderPayMethod":
      return payMethod;
    default:
      return auth;
  }
});
</script>
<template>
  <component :is="step" @close="handleCloseOrder" />
</template>
