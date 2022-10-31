<template>
  <view class="menu-list">
    <view
      class="menu-list__bg"
      :style="{
        transform: `translate(${isRight ? '70%' : '-70%'}, -50%)`,
        [isRight ? 'right' : 'left']: 0,
      }"
    ></view>
    <swiper
      :current="current"
      circular
      vertical
      skip-hidden-item-layout
      :display-multiple-items="DISPLAY_MULTIPLE_ITEMS"
      class="menu-list__inner"
      @change="current = $event.detail.current"
    >
      <swiper-item v-for="(item, index) of currentList" :key="`item-${index}`">
        <view class="menu-item" @click="onClick(index, item.index)">
          <view class="menu-item__inner" :style="style(index)">{{ item.name }}</view>
        </view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script lang="ts" setup>
import { computed } from 'vue';
import { ref, watch } from 'vue';

interface MenuItem {
  name: string;
  index: number;
}

const props = defineProps<{
  list: string[];
  isRight?: boolean;
}>();

const DISPLAY_MULTIPLE_ITEMS = 9;
const currentList = computed(() => {
  const arr: MenuItem[] = [];
  if (props.list.length) {
    while (arr.length <= DISPLAY_MULTIPLE_ITEMS) {
      arr.push(...props.list.map((name, index) => ({ name, index })));
    }
  }

  return arr;
});
const current = ref(0);
watch(currentList, (newVal) => (current.value = newVal.length - 4), { immediate: true });

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

  return {
    transform: `scale(${Math.max(0.2, 1 - 0.15 * x)})`,
    transformOrigin: `${props.isRight ? 'right' : 'left'} center`,
  };
};

const emit = defineEmits<{
  (event: 'click-item', index: number): void;
}>();
const onClick = (index: number, itemIndex: number) => {
  index -= Math.floor(DISPLAY_MULTIPLE_ITEMS / 2);
  if (index < 0) {
    index += currentList.value.length;
  }
  if (index !== current.value) {
    return (current.value = index);
  }

  emit('click-item', itemIndex);
};
</script>

<style lang="scss" scoped>
.menu-list {
  height: 100%;
  display: flex;
  align-items: center;
  position: relative;

  &__bg {
    position: absolute;
    height: 110%;
    width: 350%;
    background-color: rgba(255, 255, 255, 0.6);
    border-radius: 50%;
    top: 50%;
  }

  &__inner {
    width: 400rpx;
    height: 80%;
    flex-shrink: 0;
  }
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
