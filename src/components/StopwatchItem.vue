<template>
  <div class="container_item" :style="{'--active-color': activeColor }">
    <div class="stopwatch_container stopwatch_container_time">
      <span v-if="hours > 0">
        {{ hours }}:
      </span>
      <span v-if="minutes > 0">
      {{ minutes }}:
    </span>
      <span v-if="seconds >0">
      {{ seconds }}
    </span>
      <span v-else>00</span>
    </div>
    <hr class="hr"/>
    <div class="stopwatch_container stopwatch_container_buttons">
      <div class="button_play" v-if="!active" @click="startTimer"></div>
      <div class="button_pause" v-else @click="pauseTimer"></div>
      <div class="button_stop" @click="stopTimer"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StopwatchItem",
  data() {
    return {
      active: false,
      startTime: 0,
      activeTime: 0,
      interval: null
    }
  },
  methods: {
    startTimer() {
      this.active = true;
      this.startTime = new Date().getTime() - this.activeTime * 1000;
      this.interval = setInterval(() => {
        this.activeTime = Math.floor((new Date().getTime() - this.startTime) / 1000);
      }, 1000);
    },
    pauseTimer() {
      clearInterval(this.interval);
      this.active = false;
    },
    stopTimer() {
      clearInterval(this.interval);
      this.active = false;
      this.activeTime = 0;
      this.startTime = 0;
    }
  },
  computed: {
    seconds() {
      const time = this.activeTime % 60
      return this.hours === 24
          ? '00'
          : (time > 9
              ? time
              : `0${time}`);
    },
    minutes() {
      const time = Math.floor((this.activeTime % 3600) / 60);
      return this.hours === 24
          ? '00'
          : (time > 9
              ? time
              : `0${time}`);
    },
    hours() {
      const time = Math.floor(this.activeTime / 3600);
      if (time === 24) {
        this.stopTimer();
      }
      return time > 24 ? 24 : time;
    },
    activeColor() {
      return this.active ? 'white' : '#9E9E9E';
    }
  }
}
</script>

<style scoped>

.container_item {

  --active-color: #9E9E9E;

  width: 225px;
  height: 120px;

  display: flex;
  flex-direction: column;

  background: #696969;
}

.hr {
  border: 1px solid var(--active-color);
}

.stopwatch_container {
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.stopwatch_container_time {
  color: var(--active-color);
  font-size: 22px;
}

.stopwatch_container_buttons {
  display: flex;
  flex-direction: row;
  column-gap: 48px;
}

.button_play {
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-left: 17px solid var(--active-color);
  border-bottom: 10px solid transparent;

  cursor: pointer;
}

.button_stop {
  width: 20px;
  height: 20px;
  background: var(--active-color);

  cursor: pointer;
}

.button_pause {
  width: 10px;
  height: 20px;
  border-right: 3px solid var(--active-color);
  border-left: 3px solid var(--active-color);

  cursor: pointer;
}

</style>