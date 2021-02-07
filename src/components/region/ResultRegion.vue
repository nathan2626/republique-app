<script>

import {IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent} from "@ionic/vue";

export default {
  name: 'ResultRegion',
  data () {
    return {
      displayResult: false,
      resultRegion: "",
      cityInputRegion: "",
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
    this.$bus.on('resultRegion', (resultRegion) => {
      this.displayResult = true;
      this.resultRegion = resultRegion;
      // console.log('ici ' + ...this.resultRegion)
    })
    this.$bus.on('cityInputRegion', (cityInputRegion) => {
      this.cityInputRegion = cityInputRegion;
      // console.log(this.result)
    })
  }
};

</script>

<template>
  <div v-if="displayResult === true && isNaN(this.cityInputRegion)" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultRegion" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-subtitle><b>Code de la région :</b> {{ soloCard.code }}</ion-card-subtitle>
        <ion-card-title><b>Nom de la région :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <b>_score :</b> {{ soloCard._score }}<br>
      </ion-card-content>
    </ion-card>
  </div>

  <div v-else-if="displayResult === true && isNaN(this.cityInputRegion) === false" class="contentResult">
    <ion-card color="light" v-for="soloCard in resultRegion" :key="soloCard.nom" class="ion-padding-bottom">
      <ion-card-header>
        <ion-card-subtitle><b>Code de la région :</b> {{ soloCard.code }}</ion-card-subtitle>
        <ion-card-title><b>Nom de la région :</b> {{ soloCard.nom }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
      </ion-card-content>
    </ion-card>
  </div>
</template>