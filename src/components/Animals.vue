<template>
  <div class="animals">
    <Animal v-for="animal in animals" v-bind:animal="animal"></Animal>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
  import Animal from '@/components/Animal.vue';

  @Component({
    components: {
      Animal,
    },
  })
  export default class Animals extends Vue {
    public animals = [
      'rat',
      'cow',
      'tiger',
      'rabbit',
      'dragon',
      'snake',
      'horse',
      'goat',
      'monkey',
      'rooster',
      'dog',
      'pig',
    ];
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .animals {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
  }
</style>
