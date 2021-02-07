<script>

import {IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent} from "@ionic/vue";

export default {
  name: 'ResultDepartement',
  data () {
    return {
      displayResult: false,
      resultDepartement: "",
      cityInputDepartement: "",
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
    this.$bus.on('resultDepartement', (resultDepartement) => {
      this.displayResult = true;
      this.resultDepartement = resultDepartement;
      // console.log(this.result)
    })
    this.$bus.on('cityInputDepartement', (cityInputDepartement) => {
      this.cityInputDepartement = cityInputDepartement;
      // console.log(this.result)
    })
  }
};

</script>

<template>
  <div v-if="displayResult === true && isNaN(this.cityInputDepartement)" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultDepartement" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-subtitle><b>Code du département :</b> {{ soloCard.code }}</ion-card-subtitle>
        <ion-card-title><b>Nom du département :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <b>Code de la région :</b> {{ soloCard.codeRegion }}<br>
        <b>_score :</b> {{ soloCard._score }}<br>
      </ion-card-content>
    </ion-card>
  </div>

  <div v-else-if="displayResult === true && isNaN(this.cityInputDepartement) === false" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultDepartement" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-subtitle><b>Code du département :</b> {{ soloCard.code }}</ion-card-subtitle>
        <ion-card-title><b>Nom du département :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <b>Code de la région :</b> {{ soloCard.codeRegion }}<br>
      </ion-card-content>
    </ion-card>
  </div>
</template>