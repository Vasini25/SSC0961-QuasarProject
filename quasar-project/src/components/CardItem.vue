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
                />
              
              <q-input v-model="corrida.text" @keyup.enter="submitComent(corrida)" color="secondary" label="Adicionar comentário" style="width: 400px"/>
              <q-card v-show="corrida.newComent" class="comment-card"> {{ corrida.coment }}</q-card>
            </q-item-section>
          </q-expansion-item>
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>
  
<script>
import { ref, onMounted, watch } from 'vue';

export default {
  props: {
    raceList: {
      type: Array,
      required: true,
    },
  },

  setup(props) {
    const localRaceList = ref([]);

    // Carrega a lista de corridas do Armazenamento Local ao montar o componente
    onMounted(() => {
      loadFromLocalStorage();
    });

    // Monitora mudanças na propriedade raceList e atualiza a cópia localRaceList
    watch(() => props.raceList, (newVal) => {
      localRaceList.value = newVal;
      saveToLocalStorage(); // Salva as alterações no Armazenamento Local
    });

    // Função para salvar a cópia localRaceList no Armazenamento Local
    const saveToLocalStorage = () => {
      localStorage.setItem('raceList', JSON.stringify(localRaceList.value));
    };

    // Função para carregar a lista de corridas do Armazenamento Local para a cópia localRaceList
    const loadFromLocalStorage = () => {
      const savedRaceList = localStorage.getItem('raceList');
      if (savedRaceList) {
        localRaceList.value = JSON.parse(savedRaceList);
      } else {
        // Se não houver dados salvos, inicialize a lista com os dados da prop raceList
        localRaceList.value = props.raceList;
      }
    };

    const submitComent = (corrida) => {
      corrida.coment = corrida.text;
      corrida.newComent = true;
      corrida.text = '';
      saveToLocalStorage(); // Salva as alterações no Armazenamento Local
    };

    const getIcon = (iconName, corrida) => {
      // Retorna o nome do ícone a ser exibido com base no valor da checkbox (corrida.val)
      return corrida.val ? iconName : "star_border";
    };

    return {
      localRaceList,
      coment: '',
      newComent: false,
      text: ref(''),
      val: ref(false),
      submitComent,
      getIcon,
    };
  },
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

  .comment-card {
    background-color: whitesmoke;
    color: 3f3b3b;
    border: 1px solid #fe1b1b;
    max-width: 400px;
    min-height: 30px;
    text-align: center;
    margin-top: 10px;
  }

  .shadows {
    box-shadow: 5px 5px 7px #444444;
  }

</style>