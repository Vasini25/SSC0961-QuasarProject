<template>
  <div class="row inline justify-between items-baseline content-around">
    <div class="col-4" v-for="(corrida, index) in raceList" :key="index">
      <q-card class="q-card--bordered custom-card shadows q-mb-sm">
        <q-card-section>
          <q-expansion-item 
            :label= corrida.raceName
            :caption=corrida.date
            >
            <q-item-section class="espacamento-col">
              
              <q-item-label label>
                Circuito: {{ corrida.Circuit.circuitName }}
              </q-item-label>
              <q-item-label label>
                Data: {{ corrida.date }}
              </q-item-label>
              <q-item-label label>
                Horário: {{ corrida.time }} (UTC)
              </q-item-label>
              
              <q-checkbox
                left-label
                v-model="corrida.val" 
                checked-icon="star"
                unchecked-icon="star_border"
                label="Like"
                indeterminate-icon="star_border"
                size="45px"
                style="font-size: medium;"
                color="orange"
                @change="saveCheckboxState"
              />

            </q-item-section>
          </q-expansion-item>
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>
  
<script>
import { ref, onMounted} from 'vue'

  export default {
    props: {
      raceList: {
        type: Array,
        required: true,
      },
    },

    
    setup() {
      const corrida = ref({ val: false });
    }
  };
</script>
  
<style>
  
  .espacamento-col
  {
    margin-top: 20px;
    margin-left: 15px;
    margin-right: 15px;
  }

  .custom-card {
    background-color: whitesmoke;
    color: 3f3b3b;
    border: 1px solid #fe1b1b;
    max-width: 500px;
    margin-top: 20px;
  }

  .shadows {
    box-shadow: 5px 5px 7px #444444;
  }

</style>