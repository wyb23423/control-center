<template>
  <swiper
    class="page-container"
    :current="current"
    display-multiple-items="3"
    @change="current = $event.detail.current"
  >
    <swiper-item></swiper-item>
    <swiper-item>
      <view class="module-item" :style="style(0)">
        <view class="module-item__inner" style="background-image: url(/static/bg/Place/2022.1.22.png)" @click="go(0)">
          背景音乐
        </view>
      </view>
    </swiper-item>
    <swiper-item>
      <view class="module-item" :style="style(1)">
        <view class="module-item__inner" style="background-image: url(/static/bg/Place/2022.1.21.png)" @click="go(1)">
          监控中心
        </view>
      </view>
    </swiper-item>
    <swiper-item>
      <view class="module-item" :style="style(2)">
        <view class="module-item__inner" style="background-image: url(/static/bg/Place/2022.3.31.png)" @click="go(2)">
          智能门禁
        </view>
      </view>
    </swiper-item>
    <swiper-item item-id="3"></swiper-item>
  </swiper>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const current = ref(1);

const style = (index: number) => {
  return { transform: `scale(${1 - 0.2 * Math.abs(index - current.value)})` };
};

const go = (index: number) => {
  if (index !== current.value) {
    return (current.value = index);
  }

  const urls = ['/pages/background-music', '/pages/monitoring-center', '/pages/entrance-guard'];
  uni.navigateTo({ url: urls[index] });
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
