<template>
  <div>
    <div>{{ formatTime }}</div>
    <button @click="toggleTimer">{{ isCounting ? "暂停" : "开始" }}</button>
    <button @click="resetTimer">重置</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCounting: false,
      startTime: null,
      currentTime: 0,
      timer: null,
    };
  },
  computed: {
    formatTime() {
      const minutes = Math.floor(this.currentTime / 60);
      const seconds = this.currentTime % 60;
      return `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(
        2,
        "0"
      )}`;
    },
  },
  methods: {
    toggleTimer() {
      if (this.isCounting) {
        clearInterval(this.timer);
      } else {
        this.startTime = Date.now() - this.currentTime * 1000;
        this.timer = setInterval(this.updateTime, 1000);
      }
      this.isCounting = !this.isCounting;
    },
    resetTimer() {
      this.isCounting = false;
      clearInterval(this.timer);
      this.startTime = null;
      this.currentTime = 0;
    },
    updateTime() {
      this.currentTime = Math.floor((Date.now() - this.startTime) / 1000);
      if (this.currentTime >= 60) {
        clearInterval(this.timer);
        this.playAudio();
      }
    },
    playAudio() {
      const audio = new Audio("path_to_audio_file.mp3");
      audio.play();
    },
  },
};
</script>
