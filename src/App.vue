<template>
  <div class="main">
    <countdown />
    <img
      :src="require(`@/assets/${devicePath}/banner.png`)"
      class="banner"
      alt="banner"
    />
    <red-envelope />
    <hot-lesson />
    <lucky-bag />
    <img
      :src="require(`@/assets/${devicePath}/footer.png`)"
      class="footer"
      alt="footer"
    />
  </div>
</template>

<script>
import { defineComponent, ref, provide } from 'vue';
// import HelloWorld from './components/HelloWorld.vue';
import RedEnvelope from './components/RedEnvelope.vue';
import Countdown from './components/Countdown.vue';
import HotLesson from './components/HotLesson.vue';
import LuckyBag from './components/LuckyBag.vue';

export default defineComponent({
  name: 'App',
  components: {
    Countdown,
    RedEnvelope,
    HotLesson,
    LuckyBag,
  },
  setup() {
    const devicePath = ref('mobile');
    provide('devicePath', devicePath);

    return {
      devicePath,
    };
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      if (window.innerWidth >= 1400) {
        this.devicePath = 'desktop';
      } else if (window.innerWidth >= 768) {
        this.devicePath = 'tablet';
      } else {
        this.devicePath = 'mobile';
      }
    },
  },
});
</script>

<style lang="scss">
@import "@/styles/variables.scss";

.main {
  max-width: 1920px;
  min-width: $mobile;
  margin: auto;
  .banner,
  .footer {
    width: 100%;
  }
  .footer {
    vertical-align: bottom;
  }
}
</style>
