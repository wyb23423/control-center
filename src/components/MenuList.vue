<template>
  <swiper
    :current="current"
    vertical
    display-multiple-items="9"
    class="menu-list"
    @change="current = $event.detail.current"
  >
    <swiper-item v-for="i of fillCount" :key="`before-${i}`"></swiper-item>
    <swiper-item v-for="(item, index) of list" :key="`item-${index}`">
      <view class="menu-item" @click="onClick(index)">
        <view class="menu-item__inner" :style="style(index)">{{ item }}</view>
      </view>
    </swiper-item>
    <swiper-item v-for="i of fillCount" :key="`after-${i}`"></swiper-item>
  </swiper>
</template>

<script lang="ts" setup>
import { ref, watch } from 'vue';

const props = defineProps<{
  list: string[];
  isRight?: boolean;
}>();

const fillCount = 4;
const current = ref(0);

const style = (index: number) => {
  return {
    transform: `scale(${1 - 0.15 * Math.abs(index - current.value)})`,
    transformOrigin: `${props.isRight ? 'right' : 'left'} center`,
  };
};

watch(
  () => props.list,
  (newVal) => (current.value = Math.floor(newVal.length / 2)),
  { immediate: true }
);

const emit = defineEmits<{
  (event: 'click-item', index: number): void;
}>();
const onClick = (index: number) => {
  if (index !== current.value) {
    return (current.value = index);
  }

  emit('click-item', index);
};
</script>

<style lang="scss" scoped>
.menu-list {
  width: 400rpx;
  height: 80%;
  flex-shrink: 0;
}

.menu-item {
  height: 100%;
  display: flex;
  align-items: center;

  &__inner {
    height: 80%;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 200ms;
    width: 100%;
    background-color: #fff;
  }
}
</style>
