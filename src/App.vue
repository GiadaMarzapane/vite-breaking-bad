<script >
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';
import axios from 'axios';
import store from './store'

  export default{
    name: 'App',

    components:{
      AppHeader,
      AppMain,
      AppFooter
    },

    data(){
      return{
        cards: [],
        store
      }
    },

    created() {
      axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
      .then((response) => {
        console.log(response.data.data.slice(0, 20));
        this.cards = response.data.data.slice(0, 20);
      }
      );
    }
  }
</script>

<template>
  <AppHeader/>
  <AppMain :cardList="cards" />
  
</template>

<style lang="scss">
  @import '../src/styles/main.scss';
</style>