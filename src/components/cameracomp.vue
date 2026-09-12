<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-button expand="block" @click="takePicture">
        <ion-icon slot="start" :icon="cameraIcon" />
        Take Picture
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p>{{ errorMessage }}</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import { ref } from "vue";
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonButton,
  IonIcon,
  IonText
} from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera, CameraResultType, CameraSource } from "@capacitor/camera";

const errorMessage = ref("");

const emit = defineEmits<{
  (event: "photoCaptured", photo: string): void;
}>();

const takePicture = async () => {
  errorMessage.value = "";
  try {
    const photo = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.Uri,
      source: CameraSource.Camera
    });

    if (photo.webPath) {
      emit("photoCaptured", photo.webPath);
    }
  } catch (error) {
    errorMessage.value = "Failed to take photo. Please try again.";
    console.error(error);
  }
};
</script>