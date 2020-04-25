<template lang="html">
  <div>
    <h2>{{card.name}}</h2>
    <img width="200px" :src="getImageURL">
    <br>
    <i>"{{card.flavor}}"</i>
    <h3>Class:</h3>
      <p>{{card.playerClass}}</p>
    <h3></h3>

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
