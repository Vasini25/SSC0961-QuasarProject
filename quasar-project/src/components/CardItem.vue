<template>
      <q-card v-for="(corrida, index) in raceList" :key="index">
        <!--{{ index + 1 }}. {{ corrida.raceName }} - {{ corrida.date }} -->
        <q-card-section>
          <q-expansion-item 
            :label= corrida.raceName
            :caption=corrida.date
            :label-class="{'font-size-1': true }"
            :caption-class="{'font-size-2': true }"
            >
            <q-item-section class="q-pa-md">
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

    computed: {
      'font-size-1': true,
    },
  };

  </script>
  
  <style>
  
  .font-size-1 {
  font-size: 64px;
  }

  .font-size-2 {
  font-size: 14px;
  }

  </style>