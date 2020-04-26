<template lang="html">
  <div id="app">
    <h1>Hearthstone Card Browser</h1>

    <form v-on:submit.prevent>
      <input type="text" v-model="search" placeholder="search for card..." v-on:keyup="searchForCard">
    </form>

    <card-list :cards="cards"></card-list>

    <card-detail v-if="selectedCard" :card="selectedCard"></card-detail>
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
		    'x-rapidapi-key': 'f69f28a03fmsh66ff563f5751cbdp1e1d75jsn810cdca72e97'
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
    max-width: 1000px;
    padding: 20px;
    border-style: ridge;
    border-width: 10px;
    background-color: burlywood;
  }

  h1, h2, h3, p, i {
    font-family: 'Almendra SC', serif;
  }

</style>
