<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Communes</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="doRefresh($event)">
        <ion-refresher-content
            :pulling-icon="chevronDownCircleOutline"
            pulling-text="Tirer pour rafraichir"
            refreshing-spinner="circles"
            refreshing-text="rafraîchissant..."></ion-refresher-content>
      </ion-refresher>
      <ion-card class="ion-padding-top">
        <p style="color: #0d0d0d; font-size: 1rem;" class="ion-padding ion-text-center">
          ✅ Si votre recherche est bonne mais qu'aucun résultat n'apparaît,
          tirer vers le bas pour rafraichir. ✅</p>
        <ion-img style="width: 70%;" src="../assets/img/Communes.png"></ion-img>
        <SearchCommune />
      </ion-card>
      <ResultCommune />
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonCard, IonRefresherContent, IonRefresher, IonImg, IonToolbar, IonTitle, IonContent} from '@ionic/vue';
import ResultCommune from '../components/commune/ResultCommune.vue'
import SearchCommune from '../components/commune/SearchCommune.vue'
import {chevronDownCircleOutline} from "ionicons/icons";

export default  {
  name: 'Communes',
  data () {
    return {
      displayResult: false,
      cityInput: "",
      result: "",
    }
  },
  components: {
    ResultCommune,
    SearchCommune,
    IonHeader,
    IonToolbar,
    IonCard,
    IonRefresherContent,
    IonRefresher,
    IonImg,
    IonTitle,
    IonContent,
    IonPage,
  },
  setup() {
    const doRefresh = (event) => {
      console.log('Begin async operation');

      setTimeout(() => {
        console.log('Async operation has ended');
        event.target.complete();
        document.location.reload();

      }, 2000);
    }
    return { chevronDownCircleOutline, doRefresh }
  }
}
</script>