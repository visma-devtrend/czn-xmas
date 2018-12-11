<template>
  <div id="app">
    <h1>{{ message() }}</h1>
    <Animals v-if="!showGreeting"></Animals>
    <Greeting v-if="showGreeting"></Greeting>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
  import Animals from './components/Animals.vue';
  import Greeting from './components/Greeting.vue';
  import EventBus from '@/EventBus';

  @Component({
    components: {
      Animals,
      Greeting
    }
  })
  export default class App extends Vue {
    private showGreeting = false;

    public mounted() {
      EventBus.$on('greeting-found', () => {
        setTimeout(() => this.showGreeting = true, 500);
      });
    }

    private message() {
      return this.showGreeting ? 'Hoooray!' : `Where's the greeting?`;
    }
  }
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  body {
    background: #2C4255;
    font-family: "Open Sans", Arial, "Helvetica Neue", Helvetica, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    text-align: center;
    color: white;
  }

  p {
    padding: 15px;
    font-size: 21px;
  }
</style>
