<template lang="html">
  <div id="app">
    <h1>Hearthstone Card Browser</h1>

    <form id="search" v-on:submit.prevent>
      <input type="text" v-model="search" placeholder="search for card..." v-on:keyup="searchForCard">
    </form>

    <card-list id="list" :cards="cards"></card-list>

    <card-detail id="detail" v-if="selectedCard" :card="selectedCard"></card-detail>
  </div>
</template>

<script>
import CardList from './components/CardList.vue';
import {eventBus} from './main.js';
import CardListItem from './components/CardListItem.vue';
import CardDetail from './components/CardDetail.vue';

export default {
  name: 'app',
  data() {
    return {
      cards: [],
      selectedCard: {},
      search: ""
    }
  },
  mounted() {
    fetch("https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/classes/Mage", {
	    method: 'GET',
	    headers: {
		    'x-rapidapi-host': 'omgvamp-hearthstone-v1.p.rapidapi.com',
		    'x-rapidapi-key': process.env.VUE_APP_API_KEY
	    }
    })
    .then(response => response.json())
    .then(cards => this.cards = cards)

    eventBus.$on('selected-card', (card) => {
      this.selectedCard = card;
    })
  },
  components: {
    'card-list': CardList,
    'card-list-item': CardListItem,
    'card-detail': CardDetail
  },
  methods: {
    searchForCard(){
      let foundCard = this.cards.find((card) => {
        return card.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedCard = foundCard

      eventBus.$emit('card-selected', this.selectedCard)
    }
  }
}
</script>


<style lang="css" scoped>

  #app {
    max-width: 1200px;
    padding: 20px;
    border-style: ridge;
    border-color: black;
    border-width: 10px;
    background-color: burlywood;
    background-image: url(https://www.eldoradostone.com/wp-content/uploads/2015/12/ES_Chiseled-Edge_Accents_prof_buckskin-color-sample-320x192.jpg);
  }

  h1 {
    margin-left: 30%;
    margin-right: 25%;
    font-family: 'Almendra SC', serif;
    font-size: 45px;
  }

  h2 {
    font-family: 'Almendra SC', serif;
  }

  h3 {
    font-family: 'Almendra SC', serif;
    font-weight: 900;
  }

  p, i {
    font-family: 'Almendra SC', serif;
    font-weight: 300;
  }

  #detail {
    padding-left: 35px;
    border-left-style: double;
    max-width: 315px;
    flex: auto;
    justify-content: flex-end;
    position: absolute;
    top: 150px;
    right: 150px;
    left: 875px;
  }

  #list {
    padding-top: 40px;
    max-width: 800px;
    font-family: 'Acme', sans-serif;
    font-weight: 400;
    font-size: 18px;
    columns: 4;
  }

  #search {
    margin-left: 45%;
    margin-right: auto;
  }

</style>
