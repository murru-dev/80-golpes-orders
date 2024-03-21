<script lang="ts" setup>
const emits = defineEmits(["close"]);
const handleClose = () => {
  emits("close");
};
</script>
<template>
  <OrderStep title="Método de Pago" :close-handler="handleClose"></OrderStep>
</template>
