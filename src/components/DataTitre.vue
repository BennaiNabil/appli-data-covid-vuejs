<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ texte }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "DataTitle",
  props: ["texte", "dateStatistiques"],
  computed: {
    timestamp() {
      moment.locale('fr');
      return moment(this.dateStatistiques).format('LLLL');
      // return moment(this.dateStatistiques, 'YYYYMMDD').fromNow(); // donne les stats "il y a X jours/heures etc"
    }
  }
}
</script>
