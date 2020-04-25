<template lang="html">
  <div>
    <h1>Hearthstone Deck Builder</h1>
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
      selectedCard: null
    }
  },
  mounted() {
    fetch("https://omgvamp-hearthstone-v1.p.rapidapi.com/cards", {
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
  }
}
</script>

<style lang="css" scoped>
</style>
