<template>
  <view class="visitor-list">
    <view class="title">近期访客列表如下：</view>
    <view v-if="!isLoading" v-for="(visitor, index) in sortedVisitorList" :key="index" class="visitor-item">
      <view class="visitor-info">
        <text class="visitor-name">{{ formatVisitorName(visitor.name) }}</text>
        <text class="visitor-time">访问于 {{ formatDate(visitor.timestamp) }}</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      visitorList: [],
      isLoading: true // 加载状态
    };
  },
  created() {
    this.showLoading(); // 显示加载动画
    setTimeout(() => {
      this.generateVisitorList();
    }, 3000); // 延迟加载 3 秒
  },
  methods: {
    showLoading() {
      uni.showLoading({
        title: '加载中...',
        mask: true
      });
    },
    generateVisitorList() {
      // 随机生成30个访客数据
      for (let i = 0; i < 30; i++) {
        const name = this.generateRandomName();
        const timestamp = this.generateRandomTimestamp();
        this.visitorList.push({ name, timestamp });
      }
      // 根据访问时间倒序排序
      this.visitorList.sort((a, b) => b.timestamp - a.timestamp);
      this.hideLoading(); // 加载完成后隐藏加载动画
    },
    hideLoading() {
      uni.hideLoading();
      this.isLoading = false; // 加载完成后更新加载状态
    },
    generateRandomName() {
      const letters = 'abcdefghijklmnopqrstuvwxyz';
      const randomFirstLetter = letters[Math.floor(Math.random() * letters.length)];
      const randomMiddleLetters = '****';
      const randomLastLetter = letters[Math.floor(Math.random() * letters.length)];
      return randomFirstLetter + randomMiddleLetters + randomLastLetter;
    },
    generateRandomTimestamp() {
      const today = new Date();
      const tenDaysAgo = new Date(today.getTime() - 10 * 24 * 60 * 60 * 1000); // 十天前的时间
      const randomTimestamp = Math.floor(tenDaysAgo.getTime() + Math.random() * (today.getTime() - tenDaysAgo.getTime()));
      return randomTimestamp;
    },
    formatVisitorName(name) {
      return name;
    },
    formatDate(timestamp) {
      const date = new Date(timestamp);
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();
      const hours = date.getHours();
      const minutes = date.getMinutes();
      const seconds = date.getSeconds();
      return `${year}年${month}月${day}日 ${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }
  },
  computed: {
    sortedVisitorList() {
      return this.visitorList;
    }
  }
}
</script>

<style scoped>
/* 样式根据需求自行调整 */
.visitor-list {
  padding: 20px;
}

.title {
  text-align: center;
  font-size: 18px;
  margin-bottom: 10px;
}

.visitor-item {
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  background-color: #f5f5f5;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: center; /* 居中显示 */
}

.visitor-info {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.visitor-name {
  font-size: 16px;
  font-weight: bold;
}

.visitor-time {
  font-size: 14px;
  color: #666666;
}
</style>
