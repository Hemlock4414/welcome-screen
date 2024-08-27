

<template>
 
 <header>
        <div class="topline">Welcome to Opportunity</div>

        <div class="date"> {{ currentDate }} </div>
  </header>

  <main>
  
    <MonitorCard
      v-for="(row, index) in sheetData.slice(1)"
      :key="index"
      :topText="row[0]"
      :middleText="row[1]"
      :bottomText="row[2]"
    />
    <LiveTicker 
    v-if="tickerMessage"
    :tickerMessage="tickerMessage" 
    :speed="10" 
    />
  </main>

  <footer>

    <div class="footer-container">
      <img src="/STZH_SEB_Logo-2.png" alt="">
      <img src="/Opportunity.png" alt="">
      <img src="/SAG_Logo_De.png" alt="">
    </div>
  </footer>

</template>

<script>
import { nextTick } from 'vue';

import MonitorCard from '@/components/MonitorCard.vue';
import LiveTicker from '@/components/LiveTicker.vue';

export default {
  components: {
    MonitorCard,
    LiveTicker
  },
  data() {
    return {
      currentDate: this.getCurrentDate(),
      sheetData: [], // Hier werden die Daten vom Google Sheet gespeichert
      tickerMessage: "" 
    };
  },
  methods: {
    getCurrentDate() {
      const options = {
        day: '2-digit',
        month: '2-digit',
        year: 'numeric'
      };
      return new Date().toLocaleDateString('de-DE', options);
    },
    updateDateEveryHour() {
      this.currentDate = this.getCurrentDate();
      setInterval(() => {
        this.currentDate = this.getCurrentDate();
      }, 3600000); // Aktualisiert jede Stunde
    },
    async getData() {
      try {
        const googleAPI = import.meta.env.VITE_GOOGLE_API_KEY;
        const googleSheetId = import.meta.env.VITE_GOOGLE_SHEET_ID;

        const response = await fetch(`https://sheets.googleapis.com/v4/spreadsheets/${googleSheetId}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${googleAPI}`);
        // Backticks und keine single Quotes bei Variablen in der URL
        const data = await response.json();
        this.sheetData = data.valueRanges[0].values;
        // console.log('Fetched Data:', data);

        // Setze die erste Nachricht des Tickers, falls vorhanden
        if (this.sheetData.length > 0 && this.sheetData[0].length > 4) {
          // > 0 -> Überprüft, ob mesindestens eine Zeile in den abgerufenen Daten gibt. 
          // > 4 -> Überprüft, ob diese erste Zeile mindestens 5 Spalten enthält.
        this.tickerMessage = this.sheetData[1][4]; // Zweite Zeile, fünfte Spalte
          } else {
            this.tickerMessage = "";
          }

          nextTick(() => {
          this.startTicker(); // Start ticker after data is set
          });
      } catch (error) {
        console.error('Error fetching Google Sheet data:', error);
      }
      // console.log(this.tickerMessage);

    }
  },
  mounted() {
    this.updateDateEveryHour();
    this.getData();
    setInterval(this.getData, 60000); // Aktualisiert die Daten jede Minute
  }
};
</script>

<style scoped>
</style>
