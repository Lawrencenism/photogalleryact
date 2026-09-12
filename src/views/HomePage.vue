<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <CameraComponent @photo-captured="addPhoto" />
      <PhotoGalleryComponent :photos="photos" />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent
} from "@ionic/vue";
import CameraComponent from "@/components/cameracomp.vue";
import PhotoGalleryComponent from "@/components/photogallerycomp.vue";

const photos = ref<string[]>([]);

const addPhoto = (photo: string) => {
  photos.value.unshift(photo);
};
</script>