<template>
  <ion-page>
    <ion-header>
      <ion-toolbar mode="ios">
        <ion-back-button
          :icon="chevronBackOutline"
          default-href="/tabs/home"
          mode="md"
          slot="start"
        ></ion-back-button>
        <div class="search">
          <div class="relative" dir="ltr">
            <input
              type="text"
              class="h-12 w-full pl-10 pr-20 rounded-full z-0 focus:shadow focus:outline-none"
              placeholder="ابحث عن منتج"
              @click="seacrh()"
            >
            <div class="absolute top-2 right-2">
              <button class="p-2 text-white rounded-full bg-red-500 hover:bg-red-600">
                <svg
                  class="h-4 w-8 fill-current"
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  version="1.1"
                  id="Capa_1"
                  x="0px"
                  y="0px"
                  viewBox="0 0 56.966 56.966"
                  style="enable-background:new 0 0 56.966 56.966;"
                  xml:space="preserve"
                  width="512px"
                  height="512px"
                >
                  <path
                    d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-item>
        <ion-label>
          <i class="fi fi-rr-filter"></i>
        </ion-label>
        <ion-select
          :interface-options="customActionSheetOptions"
          interface="action-sheet"
          placeholder="السعر "
        >
          <ion-select-option value="red">من الاعلي الي الاقل</ion-select-option>
          <ion-select-option value="purple">من الاقل الي الاعلي</ion-select-option>
        </ion-select>
      </ion-item>
    </ion-content>
  </ion-page>
</template>
<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonContent,
  IonBackButton,
  IonItem,
  IonLabel,
  IonSelect,
  IonSelectOption
} from "@ionic/vue";
import { chevronBackOutline } from "ionicons/icons";

export default {
  name: "search",
  setup() {
    return {
      chevronBackOutline
    };
  },
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonContent,
    IonBackButton,
    IonItem,
    IonLabel,
    IonSelect,
    IonSelectOption
  }
};
</script>

