<template>
  <view class="page-container">
    <bing-progress
      :value="voice"
      direction="vertical"
      no-active-color="#f1f1f1"
      stroke-width="10px"
      width="60vh"
      active-color="#9999FF"
      handle-color="#9999FF"
      handle-width="10px"
      handle-height="30px"
      border-radius="10px"
      class="volume-control"
      @dragend="onVoiceChange($event.value)"
    ></bing-progress>

    <view class="music-container">
      <view class="music-title">音乐列表</view>
      <scroll-view scroll-y class="music-list" :scroll-into-view="`music-${current}`">
        <view
          v-for="(item, index) of music"
          :id="`music-${index}`"
          :key="item.id"
          :class="['music-item', { active: index === current }]"
          @click="switchCurrent(index)"
        >
          <view class="music-index">{{ index + 1 }}</view>
          <view class="music-name">{{ item.name }}</view>
        </view>
      </scroll-view>
    </view>
    <view class="controls">
      <text :class="['iconfont', `icon-${loopType}`]" @click="switchLoopType"></text>
      <text class="iconfont icon-shangyishou_huaban" @click="playNext(-1)"></text>
      <text :class="['iconfont', `icon-${isPlaying ? 'iconstop' : '24gf-play'}`]" @click="playMusic(!isPlaying)"></text>
      <text class="iconfont icon-xiayishou_huaban" @click="playNext(1)"></text>
    </view>
  </view>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const isPlaying = ref(false);
const playMusic = (play: boolean) => {
  isPlaying.value = play;
};

const music = ref([
  { name: 'music1', id: 1 },
  { name: 'music2', id: 2 },
  { name: 'music3', id: 3 },
  { name: 'music4', id: 4 },
  { name: 'music5', id: 5 },
  { name: 'music6', id: 6 },
  { name: 'music7', id: 7 },
  { name: 'music8', id: 8 },
  { name: 'music9', id: 9 },
]);
const current = ref(0);
const switchCurrent = (index: number) => {
  current.value = index;
  playMusic(true);
};
const playNext = (incremental: number) => {
  let index = current.value + incremental;
  if (index > music.value.length - 1) {
    index = 0;
  } else if (index < 0) {
    index = music.value.length - 1;
  }

  switchCurrent(index);
};

const voice = ref(50);
const onVoiceChange = (value: number) => {
  if (value !== voice.value) {
    console.log(value, 'onVoiceChange');
    voice.value = value;
  }
};

enum LOOP_TYPE {
  LIST = 'liebiaoxunhuan',
  SINGEL = 'danquxunhuan',
  RANDOM = 'suijibofang',
}
const loopType = ref(LOOP_TYPE.LIST);
const switchLoopType = () => {
  const types = [LOOP_TYPE.LIST, LOOP_TYPE.RANDOM, LOOP_TYPE.SINGEL];
  const index = types.indexOf(loopType.value);
  loopType.value = types[index === types.length - 1 ? 0 : index + 1];
};
</script>

<style lang="scss" scoped>
.page-container {
  padding-top: 25vh;
  padding-left: 26vw;
  box-sizing: border-box;
  display: block;

  /* #ifdef H5 */
  padding-top: calc(25vh - 88rpx);
  /* #endif */
}

.volume-control {
  position: absolute;
  top: 50%;
  left: 60rpx;
  transform: translateY(-50%);
}

.music-container {
  width: 50vw;
  height: 45vh;
  border-radius: 40rpx;
  background-color: rgba(255, 255, 255, 0.6);
  display: flex;
  flex-direction: column;
  padding: 36rpx;
  box-sizing: border-box;
}

.music-title {
  font-size: 40rpx;
  font-weight: 700;
  text-align: center;
  margin-bottom: 24rpx;
}

.music-list {
  height: 1px;
  flex: 1;
}

.music-item {
  height: 88rpx;
  font-size: 32rpx;
  display: flex;
  align-items: center;

  &.active .music-name {
    color: #e00;
  }
}

.music-index {
  color: #666;
  margin-right: 40rpx;
}

.controls {
  margin-top: 100rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 200rpx;
  width: 50vw;

  .iconfont {
    font-size: 64rpx;
    color: #fff;
  }
}
</style>
