<script setup lang="ts">
import PassCard from "@/components/PassCard.vue";
import {computed} from "vue";

interface IAddress {
  name: string,
  address: string
}
interface ICard {
  name: string,
  title: string,
  logo: string,
  background: string
  qr_code: string,
  addresses: IAddress[],
}

const cards: ICard[] = [
  {
    name: 'mts',
    title: 'МТС',
    logo: '/mts-logo.png',
    background: '/mts-bg.png',
    qr_code: '/mts-qr-code.png',
    addresses: [
      {
        name: 'Офис Декарт',
        address: 'Москва, Дмитровское шоссе, 19 к2'
      },
      {
        name: 'Офис Декарт',
        address: 'Москва, Дмитровское шоссе, 19 к2'
      }
    ]
  },
  {
    name: 'ozon',
    title: 'Ozon',
    logo: '/ozon-logo.png',
    background: '/ozon-bg.png',
    qr_code: '/ozon-qr-code.png',
    addresses: [
      {
        name: 'Офис Декарт',
        address: 'Москва, Дмитровское шоссе, 19 к2'
      },
      {
        name: 'Офис Декарт',
        address: 'Москва, Дмитровское шоссе, 19 к2'
      }
    ]
  }
]

const cardImages = computed(() => import.meta.glob('@/assets/images/cards/*', {
  eager: true,
  import: 'default',
}))
</script>

<template>
<section class="cards-list container">
  <PassCard
      v-for="(card, index) in cards"
      :data="card"
      :key="index"
      :imagesList="cardImages"
  />
</section>
</template>

<style scoped lang="scss">

.cards-list {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

</style>