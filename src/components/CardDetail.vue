<template lang="html">
  <div>
    <h2>{{card.name}}</h2>
    <img width="200px" :src="getImageURL">

    <br>

    <i v-if="card.flavor">"{{card.flavor}}"</i>

    <h3>Class:</h3>
      <p>{{card.playerClass}}</p>

    <h3>Card Set:</h3>
      <p>{{card.cardSet}}</p>

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
</style>
