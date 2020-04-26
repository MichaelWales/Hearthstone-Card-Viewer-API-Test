<template lang="html">
  <div>
    <h2>{{card.name}}</h2>
    <img width="200px" :src="getImageURL" onerror="this.src = 'https://thumbs.gfycat.com/ImaginativeCluelessCoqui-size_restricted.gif'">
    <br>
    <i v-if="card.flavor">"{{card.flavor}}"</i>

    <h3>Class:</h3>
      <p v-if="card.playerClass">{{card.playerClass}}</p>
      <p v-else>None</p>

    <h3>Card Set:</h3>
    <p v-if="card.cardSet">{{card.cardSet}}</p>
    <p v-else>N/A</p>

    <h3>Card Rarity:</h3>
      <p v-if="card.rarity">{{card.rarity}}</p>
      <p v-else>Common</p>

    <h3>Race:</h3>
      <p v-if="card.race">{{card.race}}</p>
      <p v-else>N/A</p>

    <h3>Type:</h3>
      <p v-if="card.type">{{card.type}}</p>
      <p v-else>N/A</p>

    <h3>Mana Cost:</h3>
      <p v-if="card.cost">{{card.cost}}</p>
      <p v-else>N/A</p>

    <h3>Health:</h3>
      <p v-if="card.health">{{card.health}}</p>
      <p v-else>N/A</p>

    <h3>Attack:</h3>
      <p v-if="card.attack">{{card.attack}}</p>
      <p v-else>N/A</p>

    <h3>Abilities:</h3>
      <i v-if="card.text">"{{card.text}}"</i>
      <p v-else>None</p>

  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'card-detail',
  props: ['card'],
  computed: {
    getImageURL() {
      const cardImage = this.card.cardId;
      const cardURL = 'https://art.hearthstonejson.com/v1/render/latest/enUS/256x/' + cardImage + '.png';
      return cardURL;
    }
  }
}
</script>

<style lang="css" scoped>

  h2 {
    font-family: 'Almendra SC', serif;
    font-weight: 900;
    font-size: 32px;
  }

  h3 {
    font-family: 'Almendra SC', serif;
    font-weight: 900;
    font-size: 24px;

  }

  p, i {
    font-family: 'Acme', sans-serif;
    font-weight: 200;
    font-size: 18px;
  }


</style>
