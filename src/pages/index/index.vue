<template>
  <swiper
    class="page-container"
    :current="current"
    circular
    display-multiple-items="3"
    @change="current = $event.detail.current"
  >
    <swiper-item v-for="(item, index) of currentList" :key="`item-${index}`">
      <view class="module-item" :style="style(index)">
        <view class="module-item__inner" :style="`background-image: url(${item.bg})`" @click="go(index, item.index)">
          {{ item.name }}
        </view>
      </view>
    </swiper-item>
  </swiper>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

interface MenuItem {
  name: string;
  index: number;
  bg: string;
}

const current = ref(0);
const list = [
  { name: '背景音乐', bg: '/static/bg/Place/2022.1.22.png' },
  { name: '监控中心', bg: '/static/bg/Place/2022.1.21.png' },
  { name: '智能门禁', bg: '/static/bg/Place/2022.3.31.png' },
];
const DISPLAY_MULTIPLE_ITEMS = 3;
const currentList = computed(() => {
  const arr: MenuItem[] = [];
  while (arr.length <= DISPLAY_MULTIPLE_ITEMS) {
    arr.push(...list.map((value, index) => ({ ...value, index })));
  }

  return arr;
});

const style = (index: number) => {
  const itemLength = currentList.value.length;

  let center = current.value + Math.floor(DISPLAY_MULTIPLE_ITEMS / 2);
  if (center > itemLength - 1) {
    center -= itemLength;
  }

  let x = Math.abs(index - center);
  if (x > itemLength / 2) {
    x = itemLength - x;
  }

  return { transform: `scale(${1 - 0.2 * x})` };
};

const go = (index: number, itemIndex: number) => {
  index -= Math.floor(DISPLAY_MULTIPLE_ITEMS / 2);
  if (index < 0) {
    index += currentList.value.length;
  }
  if (index !== current.value) {
    return (current.value = index);
  }

  const urls = ['/pages/background-music', '/pages/monitoring-center', '/pages/entrance-guard'];
  uni.navigateTo({ url: urls[itemIndex] });
};
</script>

<style lang="scss" scoped>
.module-item {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 200ms;

  &__inner {
    height: 50%;
    width: 80%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;

    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-size: 78rpx;
    font-weight: 700;
  }
}
</style>
