<template>
  <main v-if="!isLoading">
    <DataTitle :dateStatistiques="date" :texte="titre"/>
    <DataBoxes :statistiques="statistiques"/>
    <SelectionPays :pays="pays" @get-pays="getStatPays"/>
    <div class="flex justify-center">
      <button v-if="statistiques.Country"
              class="bg-green-700  w-1/3  text-white rounded p-3 mb-3 focus:tourline-none hover:bg-green-600"
              @click="effacerDonnees">
        Effacer données
      </button>
    </div>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Récupère les données
    </div>
    <img :src="loadingIamge"
         alt="Image sablier de chargement"
         class="w-24 m-auto">
  </main>
</template>

<script>

import DataTitle from "./DataTitre";
import DataBoxes from "./DataBoxes";
import SelectionPays from "./SelectionPays";

export default {
  name: 'Home',
  components: {
    SelectionPays,
    DataBoxes,
    DataTitle
  },
  data() {
    return {
      isLoading: true,
      titre: "Monde",
      date: '',
      statistiques: {},
      pays: [],
      loadingIamge: require('../assets/sablier.gif')
    }
  },
  methods: {
    async recupererDataCovid() {
      const response = await fetch("https://api.covid19api.com/summary");
      const data = await response.json();
      return data;
    },
    getStatPays(pays) {
      this.statistiques = pays[0];
      this.titre = `${pays[1]} ${pays[0].Country}`;
    },
    async effacerDonnees() {
      this.isLoading = true;
      const data = await this.recupererDataCovid();
      this.titre = "Monde";
      this.statistiques = data.Global;
      this.isLoading = false;
    },
  },
  async created() {
    const data = await this.recupererDataCovid();
    this.date = data.Date;
    this.statistiques = data.Global;
    this.pays = data.Countries;
    this.isLoading = false;
  },
}
</script>
