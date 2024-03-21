<script setup lang="ts">
const { loadingIndicator } = useLoading();
</script>
<template>
  <!-- Hero -->
  <Header />
  <!-- Menu -->
  <LayoutSection class="bg-menu" title="menú">
    <Menu />
  </LayoutSection>
  <!-- About -->
  <LayoutSection class="w3-black" title="nosotros">
    <div class="w3-large">
      <p>
        The Pizza Restaurant was founded in blabla by Mr. Italiano in lorem
        ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
        incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
        quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
        consequat.
      </p>
      <p>We are proud of our interiors.</p>
      <img
        src="/assets/img/onepage_restaurant.jpg"
        style="width: 100%"
        class="w3-margin-top w3-margin-bottom"
        alt="Restaurant"
      />
      <h1><b>Opening Hours</b></h1>

      <div class="w3-row">
        <div class="w3-col s6">
          <p>Mon &amp; Tue CLOSED</p>
          <p>Wednesday 10.00 - 24.00</p>
          <p>Thursday 10:00 - 24:00</p>
        </div>
        <div class="w3-col s6">
          <p>Friday 10:00 - 12:00</p>
          <p>Saturday 10:00 - 23:00</p>
          <p>Sunday Closed</p>
        </div>
      </div>
    </div>
  </LayoutSection>
  <!-- Footer -->
  <footer class="w3-center w3-black w3-padding-48 w3-large">
    <p>
      Desarrollado por
      <a
        href="https://staging-website.cp.murrudev.com/"
        title="Desarrollado por MurruDev"
        target="_blank"
        >MurruDev</a
      >
    </p>
  </footer>
</template>
<style>
.bg-menu {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-image: url("/assets/img/wave-haikei.svg");
}
</style>
