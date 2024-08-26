<script>
    export default {
        props: {

        }
    }

</script>


<template>

    <div v-for="(row, index) in sheetData.slice(1)" :key="index" class="monitor">
      <div class="inner-monitor">
    
        <div class="text-top"> {{ row[0] }} </div>
        <div class="text-middle"> {{ row[1] }} </div>
        <div class="text-bottom"> {{ row[2] }} </div>

      </div>
    </div>

</template>