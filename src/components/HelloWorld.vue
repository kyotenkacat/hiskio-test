<template>
  <div class="a"></div>
</template>

<script>
import { defineComponent, inject } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  setup() {
    const devicePath = inject('devicePath');

    return {
      devicePath,
    };
  },
  data() {
    return {
    };
  },
});
</script>

<style lang="scss" scoped>
</style>
