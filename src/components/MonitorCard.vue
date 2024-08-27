

<template>
  <div class="monitor">
    <div class="inner-monitor">
      <div class="text-top">{{ topText }}</div>
      <div class="text-middle">{{ middleText }}</div>
      <div class="text-bottom">{{ bottomText }}</div>
    </div>
  </div>
</template>

<script>
export default {
  // name: 'MonitorCard',
  props: {
    topText: {
      type: String,
      required: true
    },
    middleText: {
      type: String,
      required: true
    },
    bottomText: {
      type: String,
      required: true
    }
  }
};
</script>

<style scoped>
</style>
