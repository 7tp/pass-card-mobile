<template>
  <footer class="system-nav">
    <img height="34" src="@/assets/images/system-nav/home.png" alt="home indicator">
  </footer>
</template>

<script setup lang="ts">

</script>

<style lang="scss" scoped>

.system-nav {
  position: absolute;
  top: 778px;
  height: 34px;
  z-index: 99;
  background-color: var(--color-background);

  img {
    width: 100%;
  }
}

</style>