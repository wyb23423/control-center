<template>
  <view class="page-container">
    <MenuList :list="menus1"></MenuList>
    <scroll-view scroll-y class="guard-list">
      <view class="guard-list__inner">
        <view v-for="item of guards" :key="item.id" class="guard-item">
          {{ item.name }}
        </view>
      </view>
    </scroll-view>
    <MenuList :list="menus2" is-right></MenuList>
  </view>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import MenuList from '../components/MenuList.vue';

const menus1 = ref(['1F', '2F', '3F', '4F', '5F', '6F', '7F', '8F', '9F']);
const menus2 = ref(['1F', '2F', '3F', '4F', '5F', '6F', '7F', '8F', '9F']);

const guards = ref([
  { name: '门禁1', id: 1 },
  { name: '门禁2', id: 2 },
  { name: '门禁3', id: 3 },
  { name: '门禁4', id: 4 },
  { name: '门禁5', id: 5 },
  { name: '门禁6', id: 6 },
]);
</script>

<style lang="scss" scoped>
.guard-list {
  height: 70%;
  width: 1px;
  flex: 1;
  padding: 0 5%;

  &__inner {
    display: flex;
    align-items: center;
    gap: 45rpx;
    flex-wrap: wrap;
    width: 100%;
  }
}

.guard-item {
  height: 500rpx;
  width: calc(33.33% - 30rpx);
  background-color: #fff;
}
</style>
