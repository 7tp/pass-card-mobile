<script setup lang="ts">

import IconLogo from "@/components/icons/IconLogo.vue";
import IconProfile from "@/components/icons/IconProfile.vue";
</script>

<template>
  <div class="nav-bar-container">
    <nav class="nav-bar">
      <a href="#" class="nav-bar__logo"><IconLogo/></a>
      <a href="#" class="nav-bar__profile"><IconProfile/></a>
    </nav>
    <h1 class="title container">Мои пропуска</h1>
  </div>
</template>

<style lang="scss" scoped>

.nav-bar-container {
  position: fixed;
  top: 0;
  width: 375px;
  padding-top: 44px;
  background-color: var(--vt-c-black);
  z-index: 10;
}

.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;

  &__logo {
    height: 32px;
  }

  &__profile {
    width: 24px;
    height: 24px;
  }
}

.title {
  font-size: 32px;
  line-height: 36px;
  padding-bottom: 10px;
}

</style>