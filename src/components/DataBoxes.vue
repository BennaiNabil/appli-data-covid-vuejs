<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!--Première box-->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Cas</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nouveaux :</span>
        {{ ajouterSeparateurEspace(statistiques.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total :</span>
        {{ ajouterSeparateurEspace(statistiques.TotalConfirmed) }}
      </div>
    </div>
    <!--Deixoème box-->
    <div class="shadow-md bg-blue-200 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Morts</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nouveaux :</span>
        {{ ajouterSeparateurEspace(statistiques.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total :</span>
        {{ ajouterSeparateurEspace(statistiques.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["statistiques"],
  methods: {
    ajouterSeparateurEspace(nombre) {
      // Une regex parce que YOLO
      return nombre.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    }
  }
}
</script>
