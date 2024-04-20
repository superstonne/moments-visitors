<template>
  <view class="index">
    <view class="button-container">
      <button class="circle-button" @click="gotoVisitorList">查看访客</button>
    </view>
  </view>
</template>

<script>
export default {
  methods: {
    gotoVisitorList() {
      uni.navigateTo({
        url: '/pages/visitorList/visitorList'
      });
    }
  }
}
</script>

<style>
/* 样式根据需求自行调整 */
.index {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.button-container {
  margin-top: 20px;
}

.circle-button {
  width: 200px;
  height: 200px;
  line-height: 200px;
  border-radius: 50%;
  background-color: #007bff;
  color: #ffffff;
  font-size: 18px;
  text-align: center;
}
</style>
