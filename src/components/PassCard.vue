<template>
<div class="card" :class="[`_${data.name}`]">

  <div class="card__front" :style="styleFront">
    <div class="card__content">
      <img class="card__bg" :src="imagesList['/src/assets/images/cards' + data.background]" alt="background">
      <div class="card__header">
        <img :src="imagesList['/src/assets/images/cards' + data.logo]" :alt="'Logo ' + data.name">
        <IconInfo @click="rotate('right')" />
        <h2 class="card__title">{{data.title}}</h2>
      </div>

      <div class="card__qr">
        <img :src="imagesList['/src/assets/images/cards' + data.qr_code]" :alt="data.name + ' QR-code'">
        <div>
          Поднесите QR-код к сканирующему
          устройству
        </div>
      </div>
    </div>

    <div class="card__layers">
      <div class="layer" v-for="n in 5"></div>
    </div>
  </div>

  <div class="card__back" ref="cardBack" :style="styleBack">
    <button class="card__back-btn" @click="rotate('left')">
      <IconChevronLeft/>
      <span>{{data.title}}</span>
    </button>
    <div class="card__separator"></div>
    <div class="card__inner-container">

      <div class="card__address-container">
        <ul class="card__addresses">
          <li v-for="(address, index) in addresses"
              :key="index"
          >
            <div class="card__address-name">{{address['name']}}</div>
            <div class="card__address">{{address['address']}}</div>
          </li>
        </ul>
        <button class="card__toggle-addresses" @click="showAllAddress = !showAllAddress">
          <span v-if="showAllAddress">Скрыть адреса</span>
          <span v-else>Все адреса</span>
          <IconChevronDown :class="{'_rotate': showAllAddress}"/>
        </button>
      </div>

      <div class="card__qr">
        <img :src="imagesList['/src/assets/images/cards' + data.qr_code]" :alt="data.name + ' QR-code'">
        <div>
          Поднесите QR-код к сканирующему
          устройству
        </div>
      </div>
    </div>
  </div>

  <div class="card__right" @click="rotate('right')"></div>
  <div class="card__left" @click="rotate('left')"></div>
</div>
</template>

<script setup lang="ts">
import type {PropType} from "vue";
import {computed, ref} from "vue";
import IconInfo from "@/components/icons/IconInfo.vue";
import IconChevronLeft from "@/components/icons/IconChevronLeft.vue";
import IconChevronDown from "@/components/icons/IconChevronDown.vue";
interface IAddress {
  name: string,
  address: string
}
interface ICard {
  name: string,
  title: string,
  logo: string,
  qr_code: string,
  addresses: IAddress[],
  background: string
}

const props = defineProps({
  data: {
    type: Object as PropType<ICard>,
    required: true
  },
  imagesList: {
    type: Object,
    required: true
  }
})

const card = ref();
const cardBack = ref();
const flipIndex = ref(0);
const showAllAddress = ref(false)

const style = ref('')
const styleFront = ref('')
const styleBack = ref('')

const rotate = (dir: 'right' | 'left') => {
  dir === 'right' ? flipIndex.value++ : flipIndex.value--;
  style.value = `transform: rotateY(${.5 * flipIndex.value}turn)`;
  styleFront.value = `transform: rotateY(${.5 * flipIndex.value}turn)
    translateZ(${flipIndex.value % 2 === 1 ? -0 : 0}px)`;
  styleBack.value = `transform: rotateY(${.5 * flipIndex.value - .5}turn)
    translateZ(${flipIndex.value % 2 === 1 ? 6 : 6}px)`;
  showAllAddress.value = false;
}

const addresses = computed(() => showAllAddress.value
    ? props.data?.addresses
    : props.data?.addresses.slice(0,1));

</script>

<style scoped lang="scss">

.card {
  position: relative;
  height: 426px;
  border-radius: 16px;
  perspective: 1500px;

  &._mts &__front {
    background-color: #E40422;
  }

  &._ozon &__front {
    background-color: #1948F5;
  }

  &__right, &__left {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 20%;
    height: 60%;
    z-index: 2;
    cursor: pointer;
  }

  &__left {
    right: auto;
    left: 0;
  }

  &__layers {
    position: absolute;
    inset: 0;
    transform-style: preserve-3d;
    z-index: -1;

    .layer {
      position: absolute;
      left: 0; top: 0;
      width: 100%; height: 100%;
      border-radius: 16px;
      transform: translateZ(var(--tz));
      background-color: var(--vt-c-white);
      box-shadow: 0 0 2px #000d inset;

      @for $i from 0 to 6 {
        &:nth-child(#{$i + 1}) {
          --tz: #{($i + 1) * -1}px;
        }
      }

      &:last-child {
        box-shadow: 0 0 0.5em #000d inset, 0 0 5px #000;
      }
    }
  }

  &__front, &__back {
    position: absolute;
    width: 100%;
    height: 100%;
    padding: 20px;
    transition: transform .8s;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    border-radius: 16px;
    transform-style: preserve-3d;
  }

  &__front {
    z-index: 2;
    transform: translateZ(var(--tz));
  }

  &__back {
    background-color: var(--vt-card-back-bg);
    transform: rotateY(-.5turn) translateZ(6px);
    z-index: 2;

    .card__qr {
      margin: auto;
      color: var(--vt-c-grey);
    }
  }

  &__content {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
    padding: 20px;
    border-radius: 16px;
    overflow: hidden;
  }

  &__bg {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
  }

  &__header {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 16px;
    width: 100%;

    svg {
      position: relative;
      cursor: pointer;
      z-index: 2;
    }
  }

  &__title {
    font-size: 20px;
    line-height: 24px;
  }

  &__qr {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    width: 247px;
    font-size: 14px;
    line-height: 20px;
    text-align: center;

    img {
      width: 180px;
      height: 180px;
    }
  }

  &__back-btn {
    display: flex;
    gap: 8px;
    font-size: 20px;
    line-height: 24px;
    text-transform: uppercase;
    cursor: pointer;
  }

  &__separator {
    width: calc(100% + 40px);
    padding: 11.5px 16px;
    margin: 20px -20px 0 -20px;

    &::after {
      content: '';
      display: block;
      height: 1px;
      background-color: #67697359;
    }
  }

  &__inner-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 26px;
    height: 314px;
    overflow-y: auto;
  }

  &__address-container {
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  &__addresses {
    display: flex;
    flex-direction: column;
    gap: 4px;
    margin-top: 4px;
  }

  &__address {
    font-size: 12px;
    line-height: 16px;
  }

  &__toggle-addresses {
    display: flex;
    align-items: center;
    font-size: 14px;
    line-height: 20px;
    color: var(--vt-c-red);
    cursor: pointer;

    svg {
      transition: transform .6s;
    }

    svg._rotate {
      transform: rotate(180deg);
    }
  }
}

</style>