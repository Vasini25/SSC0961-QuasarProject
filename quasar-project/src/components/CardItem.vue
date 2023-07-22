<template>
      <q-card v-for="(corrida, index) in raceList" :key="index">
        <q-card-section>
          <q-expansion-item-label>
            {{ index + 1 }}. {{ corrida.raceName }} - {{ corrida.date }} 
          </q-expansion-item-label>
          <q-expansion-item popup caption="Clique para ver detalhes">
            <q-item-section>
              <q-item-label label>
                Nome da Corrida: {{ corrida.raceName }}
              </q-item-label>
              <q-item-label label>
                Nome do Circuito: {{ corrida.Circuit.circuitName }}
              </q-item-label>
              <q-item-label label>
                Data da corrida: {{ corrida.date }}
              </q-item-label>
              <q-item-label label>
                Horário da corrida: {{ corrida.time }} (UTC)
              </q-item-label>
            </q-item-section>
          </q-expansion-item>
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
