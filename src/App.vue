<script>

  export default {
    data() {
      return {
        currentDate: this.getCurrentDate()
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
        }, 3600000); // Aktualisiere jede Stunde
      }
    },
    mounted() {
      this.updateDateEveryHour();
    }
  };

</script>

<template>
 
 <header>
        <div class="topline">Welcome to Opportunity</div>

        <div class="date"> {{ currentDate }} </div>
    </header>

    <main>
        <div class="monitor">
            <div class="inner-monitor">
              <ul>
                <li>
                  <div class="text-top">
                    <p>14.00 Uhr</p>
                  </div>
                </li>
                <li>
                  <div class="text-middle">
                    <p>Basisbeschäftigung Besuch</p>
                  </div>
                </li>
                <li>
                  <div class="text-bottom">
                    <p>Interessierte für den zweiten Kurs werden uns besuchen</p>
                  </div>
                </li> 
              </ul>
            </div>
        </div>

        <div class="monitor"></div>
        <div class="monitor"></div>

    </main>

    <footer>
      <div class="footer-container">
        <img src="/STZH_SEB_Logo-2.png" alt="">
        <img src="/Opportunity.png" alt="">
        <img src="/SAG_Logo_De.png" alt="">
      </div>
    </footer>

</template>

<style scoped>

</style>
