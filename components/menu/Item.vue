<script lang="ts" setup>
import Modal from "../layout/Modal.vue";

const props = defineProps(["cake"]);
const emits = defineEmits(["add", "remove"]);
const handleAdd = (price: string, index: number) => {
  quantities.value[index]++;
  emits("add", parseInt(price));
};
const handleRemove = (price: string, index: number) => {
  if (quantities.value[index] > 0) {
    quantities.value[index]--;
    emits("remove", parseInt(price));
  }
};
const quantities = ref<number[]>(
  props.cake.variants.map((variant: any) => {
    return 0;
  })
);
const showModalImg = ref<boolean>(false);
const modalImg = ref<string>("");
const handleImgClick = (img: string) => {
  modalImg.value = `/${img}`;
  showModalImg.value = true;
};
const closeModalImg = () => {
  showModalImg.value = false;
  modalImg.value = "";
};
</script>
<template>
  <div class="w3-center">
    <span class="w3-xlarge">{{ cake.name }}</span>
  </div>

  <!-- Variants container -->
  <ul class="w3-ul w3-large">
    <!-- Variant -->
    <li
      v-for="(variant, index) in cake.variants"
      :key="`variant-${index}`"
      class="item"
    >
      <!-- Cake variant -->
      <div class="cake-variant">
        <img
          :src="`/${variant.img}`"
          class="w3-bar-item w3-circle cake-img"
          style="width: 85px"
          @click="handleImgClick(variant.img)"
        />
        <div class="w3-bar-item w3-margin-left brown-80-text">
          <span>{{ variant.name }}</span
          ><br />
          <span class="w3-medium">{{ variant.price }} ARS</span>
        </div>
      </div>

      <!-- Actions -->
      <div class="item-action">
        <a
          class="w3-text-green pointer"
          @click="handleAdd(variant.price, index)"
        >
          <font-awesome-icon icon="fa-solid fa-plus" class="action" />
        </a>
        <span>{{ quantities[index] }}</span>
        <a
          class="w3-text-red pointer"
          @click="handleRemove(variant.price, index)"
        >
          <font-awesome-icon icon="fa-solid fa-minus" class="action" />
        </a>
      </div>
      <Modal :show="showModalImg">
        <div
          class="w3-modal-content w3-animate-top"
          style="display: flex; justify-content: center"
        >
          <header>
            <button
              class="w3-button w3-display-topright"
              @click="closeModalImg"
            >
              <font-awesome-icon icon="fa-solid fa-xmark" class="action" />
            </button>
          </header>
          <img :src="modalImg" style="width: 100%" />
        </div>
      </Modal>
    </li>
  </ul>
</template>
<style>
.cake-img {
  cursor: pointer;
  width: 65px !important;
}
.item {
  align-items: center;
  display: flex;
  gap: 1em;
  justify-content: space-between;
}
.cake-variant {
  align-items: center;
  display: flex;
}
.item-action {
  align-items: center;
  display: flex;
  gap: 1em;
}
.action {
  width: 24px;
}
</style>
