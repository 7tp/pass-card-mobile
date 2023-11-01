<script setup lang="ts">
import StatusBar from "@/components/StatusBar.vue";
import NavBar from "@/components/NavBar.vue";
import SystemNav from "@/components/SystemNav.vue";
import PassCardsList from "@/components/PassCardsList.vue";
</script>

<template>
  <StatusBar/>
  <main class="main">
    <NavBar/>
    <PassCardsList />
  </main>
  <SystemNav/>
</template>

<style lang="scss" scoped>

.main {
  padding-top: 132px;
  padding-bottom: 48px;
  font-family: 'Aeroport', Arial, sans-serif;
}

</style>
