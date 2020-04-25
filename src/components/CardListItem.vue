<template lang="html">
  <div>
    <li v-on:click="onClick">{{card.name}}</li>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'card-list-item',
  props: ['card'],
  methods: {
    onClick() {
      eventBus.$emit('selected-card', this.card)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
