<template>
    <q-card v-for="(corrida, index) in raceList" :key="index">
      <q-card-section>
        <q-item>
          <q-item-section>
            <q-item-label>{{ corrida.raceName }}</q-item-label>
            <q-item-label caption>{{ corrida.Circuit.circuitName }} - {{ corrida.date }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-card-section>
    </q-card>
  </template>
  
  <script>
  export default {
    props: {
      raceList: {
        type: Array,
        required: true,
      },
    },
  };
  </script>  