<template>
  <!-- Apresentação dos dados após carregados -->

 <div class="q-pa-md">
    <q-select color="secondary" v-model="model" :options="options" label="Temporada" :filter="true">
      <template v-slot:prepend>
        <q-icon name="event" />
      </template>
      <q-spinner v-if="!loaded" align="right" size="25px" color="secondary" />
    </q-select>
    
    <div v-if="loaded">
      <card-item :race-list="raceList"/>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import axios from 'axios';
import CardItem from "../components/CardItem.vue";

export default defineComponent({
  name: 'IndexPage',

  components: {
    CardItem,
  },

  data() {
    return {
      model: "current",
      options: [
        'current', '2022', '2021', '2020', '2019',
        '2018', '2017', '2016', '2015', '2014', 
        '2013', '2012', '2011', '2010', '2009', 
        '2008', '2007', '2006', '2005', '2004', 
        '2003', '2002', '2001', '2000', '1999', 
        '1998', '1997', '1996', '1995', '1994', 
        '1993', '1992', '1991', '1990', '1989', 
        '1988', '1987', '1986', '1985', '1984', 
        '1983', '1982', '1981', '1980', '1979', 
        '1978', '1977', '1976', '1975', '1974', 
        '1973', '1972', '1971', '1970', '1969', 
        '1968', '1967', '1966', '1965', '1964', 
        '1963', '1962', '1961', '1960', '1959', 
        '1958', '1957', '1956', '1955', '1954', 
        '1953', '1952', '1951', '1950'
      ],

      raceList: [],
      loaded: false,
      search: '',
    };
  },

  watch: {
    model() {
      this.fetchData();
    },
  },

  created () {
    this.fetchData();
  },

  methods: {
    async fetchData() {

      try{
        this.loaded = false;

        await axios.get('http://ergast.com/api/f1/' + this.model + '.json')
        .then(response => (this.raceList = response.data.MRData.RaceTable.Races))
        .then(() => {this.loaded = true})
      }
      catch (error) {
        console.error(error);
      }
    },
  }
})
</script>

<style>
  .q-pa-md {
    padding: 12px;
    padding-left: 100px;
    padding-right: 100px;
    align-items: center;
  } 
</style>