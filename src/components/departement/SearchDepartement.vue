<template>
  <form @submit.prevent="searchCommune">
    <ion-item class="ion-text-center ion-padding-top">
      <ion-input v-model="cityInputDepartement" id="value1" placeholder="Nom du département ou son code" position="fixed" clear-input></ion-input>
    </ion-item>
    <ion-button id="buttonCity" size="block" type="submit" class="button ion-margin-top ion-text-center">
      <ion-icon  name="search-outline"></ion-icon>
    </ion-button>
  </form>
  <IonCard v-if="counterDepartement">
    {{ counterDepartement }}
  </IonCard>
</template>

<script>
import { IonInput, IonItem, IonButton, IonIcon, IonCard } from '@ionic/vue';

import axios from "axios";

export default  {
  name: 'SearchDepartement',
  data () {
    return {
      cityInputDepartement: "",
      resultDepartement: "",
      counterDepartement: "",
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
      this.$bus.emit("cityInputDepartement", this.cityInputDepartement);

      if(isNaN(this.cityInputDepartement)){
        axios
            .get(
                `https://geo.api.gouv.fr/departements?nom=${this.cityInputDepartement}&limit=5`
            )
            .then((response) => {
              this.resultDepartement = response.data;
              console.log(this.resultDepartement.length)
              // console.log(this.cityInput)
              this.counterDepartement = this.resultDepartement.length <= 1 ? ` ${this.resultDepartement.length} résultat` : ` ${this.resultDepartement.length} résultats`;

              if (this.resultDepartement.length === 0 && this.cityInputDepartement !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultDepartement", this.resultDepartement);
              }
              this.cityInputDepartement = "";
            })
            .catch((error) => {
              this.cityInputDepartement = "";
              console.log(error);
            })

      } else {

        axios
            .get(
                `https://geo.api.gouv.fr/departements?code=${this.cityInputDepartement}&limit=5`
            )
            .then((response) => {
              this.resultDepartement = response.data;
              // console.log(this.result.length)
              // console.log(this.cityInput)
              this.counterDepartement = this.resultDepartement.length <= 1 ? ` ${this.resultDepartement.length} résultat` : ` ${this.resultDepartement.length} résultats`;

              if (this.resultDepartement.length === 0 && this.cityInputDepartement !== "") {
                this.displayError("Valeur rentrée incorrecte..")
              } else {
                this.$bus.emit("resultDepartement", this.resultDepartement);
              }
              this.cityInputDepartement = "";

            })
            .catch((error) => {
              this.cityInputDepartement = "";
              console.log(error);
            })
      }

      if (!this.cityInputDepartement && typeof this.cityInputDepartement === "string") {
        this.displayError("Aucune valeur rentrée !")
      }


    }
  }
}
</script>