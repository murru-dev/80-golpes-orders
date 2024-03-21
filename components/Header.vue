<script lang="ts" setup>
const infoArr: string[] = [
  "Abierto de jueves a lunes",
  "Retiros y envíos de lunes a jueves",
  "Encargos para toda la semana",
];
</script>
<template>
  <header class="bgimg w3-display-container">
    <div class="w3-display-bottommiddle w3-padding z-index-3 tips-container">
      <span
        class="orange-80-text"
        v-for="(info, index) in infoArr"
        :key="`info-${index}`"
      >
        {{ info }}
      </span>
    </div>
    <div class="w3-display-middle w3-center z-index-3">
      <img
        src="/assets/img/hero-logo.png"
        alt="Logo Tortas 80 Golpes"
        class="hero-img"
      />
    </div>
    <div
      class="w3-overlay w3-animate-opacity absolute"
      style="cursor: pointer; display: block"
    ></div>
  </header>
</template>
<style>
.bgimg {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-image: url("/assets/img/baked-rolls.jpg");
  min-height: 90%;
}
.absolute {
  position: absolute !important;
}
.z-index-3 {
  z-index: 3;
}
.hero-img {
  width: 350px;
}
.tips-container {
  display: flex;
  flex-direction: column;
  gap: 1em;
  text-align: center;
  width: 300px;
}

@media (min-width: 768px) {
  .hero-img {
    width: 550px;
  }
  .tips-container {
    flex-direction: row;
    text-align: center;
    font-size: 18px;
    width: 700px;
  }
}

@media (min-width: 1440px) {
  .tips-container {
    font-size: 24px;
    width: 1000px;
  }
}
</style>
