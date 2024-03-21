<script lang="ts" setup>
const items = [
  {
    name: "Clásica",
    variants: [
      { name: "Torta", price: 1000, img: "cake-1.jpg" },
      { name: "Lingote", price: 1500, img: "cake-2.jpg" },
    ],
  },
  {
    name: "Membrillo",
    variants: [
      { name: "Torta", price: 2000, img: "cake-1.jpg" },
      { name: "Lingote", price: 2500, img: "cake-2.jpg" },
    ],
  },
  {
    name: "Batatona",
    variants: [
      { name: "Torta", price: 3000, img: "cake-1.jpg" },
      { name: "Lingote", price: 3500, img: "cake-2.jpg" },
    ],
  },
  {
    name: "Lemon",
    variants: [
      { name: "Torta", price: 4000, img: "cake-1.jpg" },
      { name: "Lingote", price: 4500, img: "cake-2.jpg" },
    ],
  },
  {
    name: "Chocodul",
    variants: [
      { name: "Torta", price: 5000, img: "cake-1.jpg" },
      { name: "Lingote", price: 5500, img: "cake-2.jpg" },
    ],
  },
  {
    name: "Facturera",
    variants: [
      { name: "Torta", price: 1000, img: "cake-1.jpg" },
      { name: "Lingote", price: 1500, img: "cake-2.jpg" },
    ],
  },
];
const purchaseAmount = ref<number>(0);
const addAmount = (price: number) => {
  purchaseAmount.value += price;
};
const removeAmount = (price: number) => {
  if (purchaseAmount.value > 0) {
    purchaseAmount.value -= price;
    if (purchaseAmount.value < 0) purchaseAmount.value = 0;
  }
};
const disableOrderBtn = computed(() => {
  return purchaseAmount.value === 0;
});
const showModalOrder = ref<boolean>(false);
const startOrderProcess = () => {
  showModalOrder.value = true;
};
const closeModalOrder = () => {
  showModalOrder.value = false;
};
</script>
<template>
  <div class="w3-card w3-round-large white-80-bg w3-xlarge">
    <ul class="w3-ul">
      <li v-for="(item, index) in items" :key="`item-${index}`">
        <MenuItem :cake="item" @add="addAmount" @remove="removeAmount" />
      </li>
    </ul>
  </div>
  <div class="w3-panel w3-round-large white-80-bg w3-xlarge">
    <div
      style="display: flex; align-items: center; justify-content: space-between"
    >
      <p class="capitals">total a pagar</p>
      <p class="capitals">{{ purchaseAmount.toFixed(2) }}</p>
    </div>
    <div class="w3-padding-16">
      <button
        class="w3-button w3-block orange-80-bg w3-round-large no-hover"
        :disabled="disableOrderBtn"
        @click="startOrderProcess"
      >
        Ordenar
      </button>
      <LayoutModal :show="showModalOrder">
        <Order @cancelOrder="closeModalOrder" />
      </LayoutModal>
    </div>
  </div>
</template>
<style>
.no-focus {
  outline: none !important;
}
</style>
