<template>
  <select v-model="paysSelection"
          class="form-select text-center mt-5 block w-full border p-3 rounded mb-3"
          @change="onSelectionPays">
    <option value="0">Selectionnez un pays</option>
    <option v-for="unPays in pays"
            v-bind:key="unPays.ID"
            :value="unPays.ID">{{ this.getFlagFromCountryCode(unPays.CountryCode) }} {{ unPays.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "SelectionPays",
  props: ['pays'],
  data() {
    return {
      paysSelection: 0
    }
  },
  methods: {
    // onSelectionPays va émettre le pays dans le composant Home (upward emitting) pour afficher les données
    onSelectionPays() {
      const paysSelection = this.pays.find((item) => item.ID === this.paysSelection);
      this.$emit('get-pays', [paysSelection ,this.getFlagFromCountryCode(paysSelection.CountryCode)]);
    },
    getFlagFromCountryCode(countryCode) {
      const tableCorrespondance = require('../assets/correspondance-code-drapeau.json');
      const emoji = tableCorrespondance[countryCode].emoji
      return emoji;
    }
  }
}
</script>
