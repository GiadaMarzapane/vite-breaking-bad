<script >
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';
import { store } from './store';

  export default{
    name: 'App',

    components:{
      AppHeader,
      AppMain,
    },

    data(){
      return{
        store,
        mainUrl: 'https://db.ygoprodeck.com/api/v7/cardinfo.php'
      }
    },

    methods: {
      getMyDeck(){
        axios.get(this.mainUrl)
          .then((response) => {
            this.store.deck = response.data.data.slice(0, 40);
          });
      },
      getMyArchetypes(){
        axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
          .then((response) => {
            this.store.archetypeDeck = response.data.slice(0,40);
          });
      }
    },

    created() {
      this.getMyDeck();
      this.getMyArchetypes()
    },

    computed: {

      myResearch(){
        axios.get(this.mainUrl,{
          params: {
            archetype : this.store.mySelect
          }
        })
          .then((response) => {
            this.store.deck = response.data.data;
          });
      }

    }
  }
</script>

<template>
  <AppHeader/>
  <AppMain @search="myResearch" />
  
</template>

<style lang="scss">
  @import '../src/styles/main.scss';
</style>