
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Pengaduan Mahasiswa</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <!-- <ion-button expand="block" @click="ambilData">
        Muat Ulang Data
      </ion-button> -->

      <ion-fab
  slot="fixed"
  vertical="bottom"
  horizontal="end"
>
  <ion-fab-button
    color="primary"
    :disabled="loading"
    @click="ambilData"
    aria-label="Sinkronkan data pengaduan"
  >
    <ion-icon :icon="syncOutline"></ion-icon>
  </ion-fab-button>
</ion-fab>

      <div v-if="loading">
        Memuat data pengaduan...
      </div>

      <ion-text v-else-if="error" color="danger">
        <p>{{ error }}</p>
      </ion-text>

      <ion-list v-else-if="pengaduan.length > 0">
        <ion-item v-for="item in pengaduan" :key="item.id">
          <ion-label>
            <h2>{{ item.judul }}</h2>
            <p>Nama: {{ item.nama }}</p>
            <p>NIM: {{ item.nim }}</p>
            <p>Kategori: {{ item.kategori }}</p>
            <p>Pengaduan: {{ item.isi }}</p>
            <p>Status: {{ item.status }}</p>
          </ion-label>
        </ion-item>
      </ion-list>

      <p v-else>Belum ada pengaduan.</p>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  // IonButton,
  IonFab,
  IonFabButton,
  IonIcon,
  IonList,
  IonItem,
  IonLabel,
  IonText,
  onIonViewWillEnter
} from '@ionic/vue';

import { syncOutline } from 'ionicons/icons';
interface Pengaduan {
  id: number;
  nama: string;
  nim: string;
  kategori: string;
  judul: string;
  isi: string;
  status: string;
}

const pengaduan = ref<Pengaduan[]>([]);
const loading = ref(false);
const error = ref('');

const API_URL =
  import.meta.env.VITE_API_URL ||
  'http://localhost:3000/api/pengaduan';

async function ambilData() {
  loading.value = true;
  error.value = '';

  try {
    const response = await fetch(API_URL);

    if (!response.ok) {
      throw new Error('HTTP ' + response.status);
    }

    const hasil = await response.json();

    if (!hasil.success || !Array.isArray(hasil.data)) {
      throw new Error('Format JSON tidak sesuai');
    }

    pengaduan.value = hasil.data;
  } catch (err) {
    error.value = 'Gagal mengambil data dari API.';
    console.error(err);
  } finally {
    loading.value = false;
  }
}

onIonViewWillEnter(() => {
  ambilData();
});
</script>