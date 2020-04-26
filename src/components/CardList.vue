<template lang="html">
  <div>
    <ul>
      <card-list-item id="list" v-for="(card, index) in cards" :card="card" :key="index"></card-list-item>
    </ul>
  </div>
</template>

<script>
import CardListItem from './CardListItem.vue';

export default {
  name: 'card-list',
  props: ['cards'],
  components: {
    "card-list-item": CardListItem
  }
}
</script>

<style lang="css" scoped>

  h1, h2, h3, p, i {
    font-family: 'Almendra SC', serif;
  }

  #list {
    font-family: 'Almendra SC', serif;
    list-style-type: circle;
   }

</style>
