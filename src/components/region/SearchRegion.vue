<template>
  <form @submit.prevent="searchCommune">
    <ion-item class="ion-text-center ion-padding-top">
      <ion-input v-model="cityInputRegion" id="value1" placeholder="Nom de la région ou son code" position="fixed" clear-input></ion-input>
    </ion-item>
    <ion-button id="buttonCity" size="block" type="submit" class="button ion-margin-top ion-text-center">
      <ion-icon  name="search-outline"></ion-icon>
    </ion-button>
    <ion-card v-if="counterRegion">
      {{ counterRegion }}
    </ion-card>
  </form>

</template>

<script>
import { IonInput, IonItem, IonButton, IonIcon, IonCard } from '@ionic/vue';

import axios from "axios";

export default  {
  name: 'SearchRegion',
  data () {
    return {
      cityInputRegion: "",
      resultRegion: "",
      counterRegion: ""
    }
  },
  components: {
    IonItem,
    IonInput,
    IonButton,
    IonIcon,
    IonCard
  },
  methods: {
    displayError(msg){
      const toast = document.createElement('ion-toast');
      toast.message = msg;
      toast.duration = 3000;
      toast.color = "danger";
      document.body.appendChild(toast);
      return toast.present();
    },

    searchCommune() {
      this.$bus.emit("cityInputRegion", this.cityInputRegion);

      if(isNaN(this.cityInputRegion)){
        axios
            .get(
                `https://geo.api.gouv.fr/regions?nom=${this.cityInputRegion}&limit=5`
            )
            .then((response) => {
              this.resultRegion = response.data;
              console.log(this.resultRegion.length)
              // console.log(this.cityInput)

              this.counterRegion = this.resultRegion.length <= 1 ? ` ${this.resultRegion.length} résultat` : ` ${this.resultRegion.length} résultats`;

              if (this.resultRegion.length === 0 && this.cityInputRegion !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultRegion", this.resultRegion);
              }
              this.cityInputRegion = "";
            })
            .catch((error) => {
              this.cityInputRegion = "";
              console.log(error);
            })

      } else {

        axios
            .get(
                `https://geo.api.gouv.fr/regions?code=${this.cityInputRegion}&limit=5`
            )
            .then((response) => {
              this.resultRegion = response.data;
              // console.log(this.result.length)
              // console.log(this.cityInput)
              this.counterRegion = this.resultRegion.length <= 1 ? ` ${this.resultRegion.length} résultat` : ` ${this.resultRegion.length} résultats`;

              if (this.resultRegion.length === 0 && this.cityInputRegion !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultRegion", this.resultRegion);
              }
              this.cityInputRegion = "";

            })
            .catch((error) => {
              this.cityInputRegion = "";
              console.log(error);
            })
      }

      if (!this.cityInputRegion && typeof this.cityInputRegion === "string") {
        this.displayError("Aucune valeur rentrée !")

      }


    }
  }
}
</script>