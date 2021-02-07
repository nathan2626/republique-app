<script>

import {IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent} from "@ionic/vue";

export default {
  name: 'ResultCommune',
  data () {
    return {
      displayResult: false,
      resultCommune: "",
      cityInputCommune: "",
      codesPostauxAll: "",
    }
  },
  components: {
    IonCard,
    IonCardHeader,
    IonCardSubtitle,
    IonCardTitle,
    IonCardContent,
  },
  methods: {
  },
  mounted() {
    this.$bus.on('resultCommune', (resultCommune) => {
      this.displayResult = true;
      this.resultCommune = resultCommune;
      // console.log(this.result)
    })
    this.$bus.on('cityInputCommune', (cityInputCommune) => {
      this.cityInputCommune = cityInputCommune;
      // console.log(this.result)
    })
  }
};

</script>

<template>
  <div v-if="displayResult === true && isNaN(this.cityInputCommune)" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultCommune" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-subtitle><b>Nom du département :</b> {{ soloCard.departement.nom }}</ion-card-subtitle>
        <ion-card-title><b>Nom de la commune :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <b>Nom de la région :</b> {{ soloCard.region.nom }}<br>
        <b>Code commune :</b> {{ soloCard.code }}<br>
        <b>Codes postaux :</b> {{ soloCard.codesPostaux }}<br>
        <b>Nombre d'habitants :</b> {{ soloCard.population.toLocaleString() }}
      </ion-card-content>
    </ion-card>
  </div>
  
  <div v-else-if="displayResult === true && isNaN(this.cityInputCommune) === false" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultCommune" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-title><b>Nom de la commune :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <b>Code région :</b> {{ soloCard.codeRegion }}<br>
        <b>Code Commune :</b> {{ soloCard.code }}<br>
        <b>Codes postaux :</b> {{ soloCard.codesPostaux }}<br>
        <b>Nombre d'habitants :</b> {{ soloCard.population.toLocaleString() }}
      </ion-card-content>
    </ion-card>
  </div>
</template>