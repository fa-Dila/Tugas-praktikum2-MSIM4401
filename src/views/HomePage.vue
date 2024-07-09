<template>
  <ion-page>
    <ion-content class="ion-padding" style="text-align: center">
      <ion-button @click="getData()" style="color: #fff">Get Data</ion-button>
      <table v-if="tickers.length > 0">
        <thead>
          <tr>
            <th>Name</th>
            <th>Symbol</th>
            <th>Harga USD</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="ticker in tickers" :key="ticker.id">
            <td>{{ ticker.name }}</td>
            <td>{{ ticker.symbol }}</td>
            <td>{{ ticker.price_usd }}</td>
          </tr>
        </tbody>
      </table>
      <p v-else style="color: #fff">
        Data tidak tersedia, Klik Get Data untuk menampilkan data!
      </p>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import axios from "axios";
import { ref, onMounted } from "vue";

const tickers = ref([]);

const getData = async () => {
  try {
    const response = await axios.get("https://api.coinlore.net/api/tickers/");
    tickers.value = response.data.data;
  } catch (error) {
    console.error("Error fetching tickers:", error);
  }
};

onMounted(getData);
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  background-color: #fff;
}

th,
td {
  border: 1px solid #000;
  padding: 8px;
  text-align: left;
  color: #000;
}

th {
  background-color: #f2f2f2;
}

p {
  color: #000;
}

ion-toolbar {
  text-align: center;
}
</style>
