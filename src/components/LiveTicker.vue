
<template>
    <div class="live-ticker">
      <div class="ticker-text" :style="tickerStyle">
        {{ tickerMessage }}
      </div>
    </div>
  </template>


<script>
export default {
//   name: "LiveTicker",
  props: {
    messages: {
      type: Array,
      required: true
    },
    speed: {
      type: Number,
      default: 50 // Geschwindigkeit der Bewegung, je niedriger desto schneller
    }
  },
  data() {
    return {
      tickerMessage: "",
      tickerStyle: {
        transform: "translateX(100%)"
      }
    };
  },
  methods: {
    startTicker() {
      this.tickerMessage = this.messages.join(" • "); // Verbinde die Nachrichten mit einem Trennzeichen
      const tickerWidth = this.$refs.tickerText.offsetWidth; // Breite des Tickers ermitteln
      const containerWidth = this.$refs.tickerContainer.offsetWidth; // Breite des Containers ermitteln

      let tickerPosition = containerWidth;

      const moveTicker = () => {
        tickerPosition -= 1;
        if (tickerPosition <= -tickerWidth) {
          tickerPosition = containerWidth;
        }
        this.tickerStyle.transform = `translateX(${tickerPosition}px)`;
      };

      setInterval(moveTicker, this.speed);
    }
  },
  mounted() {
    this.startTicker();
  }
};
</script>

<style scoped>
.live-ticker {
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
  background-color: #0F05A0; 
  color: #FFFFFF; 
  font-weight: bold;
}

.ticker-text {
  display: inline-block;
  padding: 10px 0;
}
</style>