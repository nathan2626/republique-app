<template>
  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>Accueil</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-card>
        <ion-img src="../assets/img/Logo_de_la_République_française.png"></ion-img>
        <ion-card-header>
          <ion-card-subtitle>"Liberté égalité fraternité !"</ion-card-subtitle>
          <ion-card-title>République App</ion-card-title>
        </ion-card-header>
        <ion-card-content class="ion-text-justify">
          République App est une application qui vous permet de rechercher des
          communes, des départements et des régions de toute la France.
        </ion-card-content>
      </ion-card>
    </ion-content>

  </ion-page>
</template>

<script>
import { IonCard, IonCardContent, IonCardSubtitle, IonCardTitle, IonCardHeader, IonPage, IonHeader, IonToolbar, IonTitle, IonContent} from '@ionic/vue';

export default  {
  name: 'Home',
  data () {
    return {
      displayResult: false,
      cityInput: "",
      result: "",
    }
  },
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonCard,
    IonCardContent,
    IonCardSubtitle,
    IonCardTitle,
    IonCardHeader,
  },
}
</script>