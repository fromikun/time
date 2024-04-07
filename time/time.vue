// 在App.vue文件中
<template>
  <div class="app">
    <div v-if="isGrey" class="grey-bg">
      <h1>番茄钟计时器</h1>
      <div class="timer">
        {{ time.minutes }}:{{
          time.seconds < 10 ? "0" + time.seconds : time.seconds
        }}
      </div>
      <button @click="toggleTimer">
        {{ isTimerRunning ? "暂停" : "开始" }}
      </button>
    </div>
    <audio ref="audio" src="completion-sound.mp3"></audio>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isGrey: true,
      isTimerRunning: false,
      time: {
        minutes: 0,
        seconds: 5,
      },
      timer: null,
    };
  },
  methods: {
    toggleTimer() {
      this.isTimerRunning = !this.isTimerRunning;
      if (this.isTimerRunning) {
        this.timer = setInterval(this.countDown, 1000);
      } else {
        clearInterval(this.timer);
      }
    },
    countDown() {
      if (this.time.minutes === 0 && this.time.seconds === 0) {
        clearInterval(this.timer);
        this.$refs.audio.play();
      } else if (this.time.seconds === 0) {
        this.time.minutes--;
        this.time.seconds = 59;
      } else {
        this.time.seconds--;
      }
    },
  },
};
</script>
<style>
.grey-bg {
  background-color: #f2f2f2;
  padding: 20px;
  text-align: center;
}
.timer {
  font-size: 40px;
  margin: 20px 0;
}
button {
  padding: 10px 20px;
  font-size: 16px;
}
</style>
```
