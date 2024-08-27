
<template>
    <div class="live-ticker" ref="tickerContainer">
      <div class="ticker-text" ref="tickerText" :style="tickerStyle">
        {{ tickerMessage }}
      </div>
      <div v-if="!tickerMessage">
        No ticker message available.
      </div>
    </div>
  </template>


<script>
import { nextTick } from 'vue';

export default {
//   name: "LiveTicker",
  props: {
    tickerMessage: {
      type: String,
      required: true
    },
    speed: {
      type: Number,
      default: 50 // Geschwindigkeit der Bewegung, je niedriger desto schneller
    }
  },
  data() {
    return {
      tickerStyle: {
        transform: "translateX(100%)"
      }
    };
  },
  methods: {
    startTicker() {
        nextTick(() => {
            const tickerWidth = this.$refs.tickerText?.offsetWidth; // Breite des Tickers ermitteln
            const containerWidth = this.$refs.tickerContainer?.offsetWidth; // Breite des Containers ermitteln

            if (!tickerWidth || !containerWidth) {
            console.error('Could not determine ticker or container width.');
            return;
            }

            let tickerPosition = containerWidth;

            const moveTicker = () => {
                tickerPosition -= 1;
                if (tickerPosition <= -tickerWidth) {
                tickerPosition = containerWidth;
                }
                this.tickerStyle.transform = `translateX(${tickerPosition}px)`;
                };
        
            setInterval(moveTicker, this.speed);
        });
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
  background-color: #ff0000; 
  color: #FFFFFF; 
  font-weight: bold;
  font-size: 50px;
}

.ticker-text {
  display: inline-block;
  padding: 10px 0;
  white-space: nowrap;
}
</style>