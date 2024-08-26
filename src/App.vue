

<template>
 
 <header>
        <div class="topline">Welcome to Opportunity</div>

        <div class="date"> {{ currentDate }} </div>
  </header>

  <main>
<!--     <div class="monitor">
        <div class="inner-monitor">
              <div class="text-top">
                <p>14.00 Uhr</p>
              </div>
              <div class="text-middle">
                <p>Basisbeschäftigung Besuch</p>
              </div>
              <div class="text-bottom">
                <p>Interessierte für den zweiten Kurs werden uns besuchen</p>
              </div>
        </div>
    </div> -->

    <Card />



    <!-- <div class="monitor"></div> -->

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
import Card from './components/Card.vue';

export default {
  data() {
    return {
      currentDate: this.getCurrentDate(),

       sheetData: [] // Hier werden die Daten vom Google Sheet gespeichert
    }
  },
  methods: {
    async getData() {
      try {
        const googleAPI = import.meta.env.VITE_GOOGLE_API_KEY
        const googleSheetId = import.meta.env.VITE_GOOGLE_SHEET_ID

        const response = await fetch(`https://sheets.googleapis.com/v4/spreadsheets/${googleSheetId}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${googleAPI}`);
        // Backticks statt singleQuotes in der URL
        const data = await response.json()
       
             console.log(response.status)
             console.log(data);

        this.sheetData = await data.valueRanges[0].values 
        // valueRanges und verschachtelt values aus dem spreadsheetId-Array

        // console.log(this.sheetData)

      } catch (error) {
        console.error('Error fetching Google Sheet data:', error);
      }
    },
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
      }, 3600000);          // Aktualisiere jede Stunde
    }
  },
  mounted() {
    this.getData(); 

    this.updateDateEveryHour();
  }
}
</script>

<style scoped>
</style>
