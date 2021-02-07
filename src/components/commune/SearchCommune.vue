<template>
  <form @submit.prevent="searchCommune">
    <ion-item class="ion-text-center ion-padding-top">
      <ion-input v-model="cityInputCommune" id="value1" placeholder="Nom de la commune ou son code" position="fixed" clear-input></ion-input>
    </ion-item>
    <ion-button id="buttonCity" size="block" type="submit" class="button ion-margin-top ion-text-center">
      <ion-icon  name="search-outline"></ion-icon>
    </ion-button>
  </form>
  <IonCard v-if="counterCommune">
    {{ counterCommune }}
  </IonCard>
</template>

<script>
import { IonInput, IonItem, IonButton, IonIcon, IonCard } from '@ionic/vue';

import axios from "axios";

export default  {
  name: 'SearchCommune',
  data () {
    return {
      cityInputCommune: "",
      resultCommune: "",
      counterCommune: "",
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
      this.$bus.emit("cityInputCommune", this.cityInputCommune);

      if(isNaN(this.cityInputCommune)){
        axios
            .get(
                `https://geo.api.gouv.fr/communes?nom=${this.cityInputCommune}&fields=departement,region,codesPostaux,population&boost=population&limit=5`
            )
            .then((response) => {
              this.resultCommune = response.data;
              console.log(this.resultCommune.length)
              // console.log(this.cityInput)

              this.counterCommune = this.resultCommune.length <= 1 ? ` ${this.resultCommune.length} résultat` : ` ${this.resultCommune.length} résultats`;


              if (this.resultCommune.length === 0 && this.cityInputCommune !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultCommune", this.resultCommune);
              }
              this.cityInputCommune = "";
            })
            .catch((error) => {
              this.cityInput = "";
              console.log(error);
            })

      } else {

        axios
            .get(
                `https://geo.api.gouv.fr/communes?codePostal=${this.cityInputCommune}`
            )
            .then((response) => {
              this.resultCommune = response.data;
              // console.log(this.result.length)
              // console.log(this.cityInput)
              this.counterCommune = this.resultCommune.length <= 1 ? ` ${this.resultCommune.length} résultat` : ` ${this.resultCommune.length} résultats`;

              if (this.resultCommune.length === 0 && this.cityInputCommune !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultCommune", this.resultCommune);
              }
              this.cityInputCommune = "";

            })
            .catch((error) => {
              this.cityInputCommune = "";
              console.log(error);
            })
      }

      if (!this.cityInputCommune && typeof this.cityInputCommune === "string") {
        this.displayError("Aucune valeur rentrée !")
      }


    }
  }
}
</script>