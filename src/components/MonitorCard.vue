

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
  margin: 40px 60px; 
  background-color: #0F05A0;
  min-height: 182px;
}

.inner-monitor {
  padding: 34.5px 35px 39.5px 35px; /* Zusammengefasst: oben/rechts/unten/links */
  min-height: 100px;
}

.text-top {
  color: #EB5E00;
  font-weight: 900;
}

.text-middle, .text-bottom { 
  color: #FFBFAB;
  font-size: 28px;
  line-height: 36px;
}

.text-middle {
  font-weight: 900;
  word-break: break-word;
}

.text-bottom {
  font-weight: 500;
}

@media (max-width: 481px) {
  header {
    font-size: 14vw;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
  }

  .topline, .date {
    margin-left: auto;
    margin-right: auto;
  }
}
</style>
