<template>
  <view class="page-container">
    <MenuList :list="menus"></MenuList>
    <view class="video-container">
      <video
        class="video"
        controls
        poster="/static/6445bfea6b447697aa6e139bb5965cab3d527514.png"
        src="/static/872755686-1-208.mp4"
      ></video>
      <scroll-view scroll-x class="video-list">
        <view class="video-list__inner">
          <view v-for="item of videoList" :key="item.id" class="video-item">
            {{ item.name }}
          </view>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import MenuList from '../components/MenuList.vue';

const menus = ref(['1F', '2F', '3F', '4F']);

const videoList = ref([
  { name: '监控1', id: 1 },
  { name: '监控2', id: 2 },
  { name: '监控3', id: 3 },
  { name: '监控4', id: 4 },
  { name: '监控5', id: 5 },
  { name: '监控6', id: 6 },
]);
</script>

<style lang="scss" scoped>
.video-container {
  width: 1px;
  flex: 1;
  height: 100%;
  padding: 120rpx;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}

.video {
  width: 100%;
  height: 70%;
}

.video-list {
  width: 100%;
  margin-top: 60rpx;
  height: 1px;
  flex: 1;

  &__inner {
    display: flex;
    align-items: center;
    gap: 40rpx;
    height: 100%;
  }
}

.video-item {
  height: 100%;
  width: 300rpx;
  flex-shrink: 0;
  background-color: #fff;
}
</style>
