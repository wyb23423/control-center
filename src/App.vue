<script setup lang="ts">
import { onLaunch, onShow, onHide } from '@dcloudio/uni-app';
onLaunch(() => {
  console.log('App Launch');
});
onShow(() => {
  console.log('App Show');
});
onHide(() => {
  console.log('App Hide');
});
</script>

<style>
@import '@/static/iconfont.css';

.page-container {
  height: 100vh;
  /* #ifdef H5 */
  height: calc(100vh - 88rpx);
  /* #endif */

  display: flex;
  align-items: center;

  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-image: url(/static/bg/bg.jpg);
}
</style>
