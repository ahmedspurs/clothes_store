<template>
  <ion-page>
    <ion-header>
      <ion-toolbar mode="ios">
        <ion-title>السله</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <div :class="{hidden:empty}" class="flex flex-col justify-center items-center h-full">
        <ion-text>
          <p>عفوا السله فارغه الرحاء اصافه بعض المنتجات اولا</p>
        </ion-text>
      </div>
      <div :class="{hidden:full}">
        <div class="cart">
          <ion-card :key="item.id" v-for="(item,index) in cart">
            <ion-card-header></ion-card-header>
            <ion-card-content>
              <div class="head flex items-center space-y-2">
                <ion-img src="abc.jpg" class="w-48"></ion-img>
                <div class="content">
                  <ion-card-title class="text-center">{{item.name}}</ion-card-title>

                  <div class="price py-4 flex justify-between items-center">
                    <ion-text color="primary" class="flex space-x-4">
                      <h2 class="text-black w-full">السعر :</h2>
                      <h2>{{item.newPrice}}$</h2>
                    </ion-text>
                  </div>
                </div>
              </div>
              <div class="flex justify-between items-center">
                <div class="qty px-2">
                  <ion-label class="text-xl px-2">الكميه</ion-label>
                  <div class="custom-number-input h-10 w-32">
                    <div class="flex flex-row h-10 w-full rounded-lg relative bg-transparent mt-1">
                      <button
                        @click="remQty(index)"
                        class="bg-gray-200 rounded-full text-gray-600 hover:text-white hover:bg-red-700 p-3 rounded cursor-pointer flex flex-col items-center justify-center"
                      >
                        <i class="fi fi-rr-minus"></i>
                      </button>
                      <input
                        type="number"
                        class="outline-none focus:outline-none text-center w-full bg-white font-semibold text-md hover:text-black focus:text-black md:text-basecursor-default flex items-center text-gray-700 outline-none"
                        v-model="item.qty"
                        min="0"
                      >
                      <button
                        @click="addQty(index)"
                        class="bg-gray-200 rounded-full text-gray-600 hover:text-white hover:bg-red-700 p-3 rounded cursor-pointer flex flex-col items-center justify-center"
                      >
                        <i class="fi fi-rr-plus"></i>
                      </button>
                    </div>
                  </div>
                </div>
                <ion-text color="primary">
                  <ion-icon @click="removeProduct(index)" class="text-2xl" :icon="trashOutline"/>
                </ion-text>
              </div>
            </ion-card-content>
          </ion-card>
        </div>

        <!-- total price section -->

        <div class="total-price">
          <ion-card>
            <ion-card-content>
              <div class="products flex justify-between">
                <ion-text color="dark">
                  <b>ملخص الطبيه</b>
                </ion-text>
                <ion-text color="dark">
                  <b>{{cart.length}} منتجات</b>
                </ion-text>
              </div>
              <div class="products flex justify-between">
                <ion-text color="dark">
                  <span>رسوم التوصيل</span>
                </ion-text>
                <ion-text color="dark">
                  <span>0$</span>
                </ion-text>
              </div>
              <div class="products flex justify-between">
                <ion-text color="dark">
                  <span>المجموع الكلي</span>
                </ion-text>
                <ion-text color="dark">
                  <span>{{totalprice()}}$</span>
                </ion-text>
              </div>
            </ion-card-content>
          </ion-card>
        </div>

        <!-- checkout section -->
        <div class="checkout p-2">
          <router-link to="/tabs/cart/checkout/">
            <ion-button expand="full">اتمام الطلب</ion-button>
          </router-link>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>
<script>
import {
  IonPage,
  IonHeader,
  IonTitle,
  IonToolbar,
  IonContent,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonButton,
  IonLabel,
  IonText,
  IonIcon,
  IonImg,
  loadingController
} from "@ionic/vue";
import { addOutline, removeOutline, trashOutline } from "ionicons/icons";
import { mapGetters } from "vuex";
export default {
  name: "cart",
  data() {
    return {
      cart: [],
      empty: true,
      full: false
    };
  },
  components: {
    IonPage,
    IonHeader,
    IonTitle,
    IonToolbar,
    IonContent,
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardTitle,
    IonButton,
    IonLabel,
    IonText,
    IonIcon,
    IonImg
  },
  methods: {
    addQty(index) {
      this.cart[index].qty++;
      this.cart[index].newPrice += this.cart[index].price;
    },
    remQty(index) {
      if (this.cart[index].qty == 0) {
        this.cart.splice(index, 1);
        if (this.cart.length == 0) {
          this.empty = !this.empty;
          this.full = !this.full;
        } else {
          this.full = false;
          this.empty = true;
        }
      } else {
        this.cart[index].qty--;
        this.cart[index].newPrice -= this.cart[index].price;
      }
    },
    removeProduct(index) {
      this.cart.splice(index, 1);
      // if (this.cart.length == 0) {
      //   this.empty = !this.empty;
      //   this.full = !this.full;
      // } else {
      //   this.full = false;
      //   this.empty = true;
      // }
    },
    totalprice() {
      let sum = 0;
      this.cart.forEach(item => {
        sum += item.newPrice;
      });
      return sum;
    },
    hello() {
      if (this.cart.length == 0) {
        this.empty = !this.empty;
        this.full = !this.full;
      } else {
        this.full = false;
        this.empty = true;
      }
    },
    async presentLoading() {
      const loading = await loadingController.create({
        cssClass: "loader",
        message:
          '<img src="https://st.depositphotos.com/47577860/52256/v/600/depositphotos_522560928-stock-illustration-loading-spanner-spinner-icon-solid.jpg" >',
        duration: 1000
      });

      await loading.present();

      setTimeout(function() {
        loading.dismiss();
      }, 1000);
    }
  },
  computed: mapGetters(["cart"]),
  created() {
    this.cart = this.$store.getters.cart;
    // this.hello()

    //   if (this.cart.length == 0) {
    //   this.empty = !this.empty;
    //   this.full = !this.full;
    // } else {
    //   this.full = false;
    //   this.empty = true;
    // }
  },
  mounted() {
    this.presentLoading();
  },
  setup() {
    return {
      addOutline,
      removeOutline,
      trashOutline
    };
  }
};
</script>

<style scoped>
</style>


