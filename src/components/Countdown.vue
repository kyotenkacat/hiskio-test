<template>
  <div id="countdown">
    <span class="word">新年快樂！還有</span>
    <span class="time">{{ countdown.day }}</span>
    <span class="word">天</span>
    <span class="time">{{ countdown.hour }}</span>
    <span class="word">時</span>
    <span class="time">{{ countdown.min }}</span>
    <span class="word">分</span>
    <span class="time">{{ countdown.sec }}</span>
    <span class="word">秒可以領紅包！</span>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Countdown',
  data() {
    return {
      countdown: {
        day: '00',
        hour: '00',
        min: '00',
        sec: '00',
      },
    };
  },
});
</script>

<style lang="scss" scoped>
@import "@/styles/variables.scss";

#countdown {
  text-align: center;
  background-color: $deep-brown;
  color: #fff;
  letter-spacing: 0.1em;
  @include rwdmax($tablet - 1) {
    height: 33px;
    line-height: 33px;
  }
  @include rwdmin($tablet) {
    height: 58px;
    line-height: 58px;
  }
  .word {
    vertical-align: text-bottom;
    @include rwdmax($tablet - 1) {
      font-size: 14px;
    }
    @include rwdmin($tablet) {
      font-size: 20px;
    }
  }
  .time {
    vertical-align: text-bottom;
    @include rwdmax($tablet - 1) {
      font-size: 18px;
      margin: 0 2px;
    }
    @include rwdmin($tablet) {
      font-size: 30px;
      margin: 0 8px;
    }
  }
}
</style>
