<template>
<header class="status-bar">
  <div class="status-bar__time">{{time}}</div>
  <img src="@/assets/images/status-bar/status-right.png" alt="status">
</header>
</template>

<script setup lang="ts">
import {onMounted, ref} from "vue";

const time = ref('0:00');

const currentTime = (() => {
  const now = new Date();
  const hours = now.getHours();
  const minutes = now.getMinutes();

  time.value = `${hours}:${minutes}`
});


onMounted(() => {
  currentTime();

  setInterval(() => {
    currentTime()
  }, 1000)
})

</script>

<style lang="scss" scoped>

.status-bar {
  position: fixed;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  width: 375px;
  padding: 12px;
  font-family: 'Gilroy', Arial, sans-serif;
  font-weight: 600;
  z-index: 99;

  &__time {
    margin-left: 16px;
    line-height: 18px;
  }

  img {
    height: 12px;
  }
}

</style>