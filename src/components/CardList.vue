<template lang="html">
  <div>
    <ul>
      <card-list-item id="list-item" v-for="(card, index) in cards" :card="card" :key="index"></card-list-item>
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

  #list-item {
    list-style-type: circle;
    padding: 5px;
  }

</style>
