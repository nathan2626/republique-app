<template>
  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>Régions</ion-title>
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
        <ion-img style="width: 70%;" src="../assets/img/region.png"></ion-img>
        <SearchRegion />
      </ion-card>
      <ResultRegion />
    </ion-content>

  </ion-page>
</template>

<script>
import { IonPage, IonCard, IonHeader, IonToolbar, IonTitle, IonContent, IonImg, IonRefresherContent, IonRefresher} from '@ionic/vue';
import ResultRegion from '../components/region/ResultRegion.vue'
import SearchRegion from '../components/region/SearchRegion.vue'
import { chevronDownCircleOutline } from 'ionicons/icons'

export default  {
  name: 'Regions',
  data () {
    return {
      displayResult: false,
      cityInput: "",
      result: "",
    }
  },
  components: {
    ResultRegion,
    SearchRegion,
    IonHeader,
    IonImg,
    IonCard,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonRefresherContent,
    IonRefresher
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