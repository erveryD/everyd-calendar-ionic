<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="home" href="/tabs/home">
          <ion-icon aria-hidden="true" :icon="homeOutline" />
          <ion-label>HOME</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="calendar" href="/tabs/calendar">
          <!-- <ion-icon aria-hidden="true" :icon="ellipse" /> -->
          <ion-icon :icon="calendarNumberOutline" />
          <ion-label>일정</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="setting" href="/tabs/setting">
          <ion-icon aria-hidden="true" :icon="settingsOutline" />
          <ion-label>설정</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
  import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue'
  import { settingsOutline, square, homeOutline, calendarNumberOutline } from 'ionicons/icons'
</script>
