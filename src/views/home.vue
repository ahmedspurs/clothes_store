<template>
  <ion-page>
    <ion-content>
      <ion-refresher slot="fixed" @ionRefresh="doRefresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>

      <search></search>
      <!-- sections of cat -->
      <main-cat></main-cat>
      <!-- categroy -->

      <cat></cat>
      <!-- marka sec -->

      <cats></cats>
      <!-- products -->

      <productsHeaeder></productsHeaeder>

      <homeProducts></homeProducts>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonContent, alertController } from "@ionic/vue";

import { arrowBackOutline, cartOutline } from "ionicons/icons";
// home components
import search from "../components/search.vue";
import mainCat from "../components/category/mainCat.vue";
import cats from "../components/category/cats.vue";
import cat from "../components/category/cat.vue";
import homeProducts from "../components/products/homeProducts.vue";
import productsHeaeder from "../components/productsHeader.vue";
import { mapGetters, mapActions } from "vuex";

export default {
  name: "home",
  components: {
    IonPage,
    IonContent,
    search,
    mainCat,
    cats,
    cat,
    homeProducts,
    productsHeaeder
  },
  data() {
    return {
      renderComponent: true
    };
  },
  setup() {
    const doRefresh = () => {
        // Remove my-component from the DOM
       location.reload()
    };
    return {
      arrowBackOutline,
      cartOutline,
      doRefresh
    };
  },
  methods: {
    ...mapActions(["fetchProducts", "fetchTypes", "fetchBrands"]),
    async presentAlert() {
      const alert = await alertController.create({
        cssClass: "my-custom-class",
        header: "تم اضافه العنصر للسله",
        message: "يمكنك التوجه للسله لاكمال الطلب",
        buttons: ["تم"]
      });
      await alert.present();
      const { role } = await alert.onDidDismiss();
      console.log("onDidDismiss resolved with role", role);
      console.log(this.allProducts, this.allTypes, this.allBrands);
    }
  },
  computed: mapGetters(["allProducts", "allTypes", "allBrands"]),
  mounted() {
    this.fetchProducts();
    this.fetchTypes();
    this.fetchBrands();
  }
};
</script>