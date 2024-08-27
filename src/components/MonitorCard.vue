

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
.monitor {
  margin-left: 60px;
  margin-right: 60px;
  margin-top: 40px;
  margin-bottom: 40px;
  background-color: #0F05A0;
  min-height: 182px;
}

.inner-monitor{
  padding-top: 34.5px;
  padding-left: 35px;
  padding-bottom: 39.5px;
  min-height: 100px;
}

.text-top {
  color: #EB5E00;
  font-weight: 900;
  font-size: 28px;
  line-height: 36px;
}

.text-middle {
  color: #FFBFAB;
  font-weight: 900;
  font-size: 28px;
  line-height: 36px;
  word-break: break-word;
}

.text-bottom {
  color: #FFBFAB;
  font-weight: 500;
  font-size: 28px;
  line-height: 36px;
}
@media (max-width: 481px) {
  header {
    font-size: 14vw;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
  }
}
@media (max-width: 481px) {
  .topline, .date {
    margin-left: auto;
    margin-right: auto;
  }
}
</style>
