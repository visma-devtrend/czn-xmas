<template>
  <span
    class="animal"
    v-on:click="open()"
    :class="classes()"
  ></span>
</template>

<script lang="ts">
  import { Component, Prop, Vue } from 'vue-property-decorator';
  import EventBus from '@/EventBus';

  @Component
  export default class Animal extends Vue {
    @Prop({ type: String }) public animal!: string;
    private isOpen = false;
    private destroy = false;

    private classes() {
      return {
        ['animal--' + this.animal]: true,
        'animal--open': this.isOpen,
        'destroy': this.destroy,
        'dog': this.isOpen && this.animal !== 'pig'
      };
    }

    private mounted() {
      EventBus.$on('greeting-found', () => {
        this.destroy = true;
      });
    }

    private open() {
      this.isOpen = !this.isOpen;

      if (this.animal !== 'pig') {
        new Audio('snort.wav').play();
        return;
      }

      new Audio('pigsnort.wav').play();

      EventBus.$emit('greeting-found');
    }
  }
</script>

<style scoped lang="scss">
  $animals: 'rat',
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
  'pig';

  .animal {
    margin: 5px;
    border: 5px solid #00a3e2;
    position: relative;
    background-size: cover;
    background-repeat: no-repeat;
    height: 128px;
    width: 100px;
    user-select: none;
    transition: transform 0.5s;
    animation: float 2s ease alternate infinite;

    @each $animal in $animals {
      &--#{$animal} {
        background-image: url("../assets/animals/#{$animal}.gif");
      }
    }

    &.dog {
      animation: none;
      background-image: url("../assets/dog.png");
      border-color: red;
    }

    &.destroy {
      animation: disappear 0.5s ease-in;
      animation-fill-mode: forwards;
    }
  }

  @keyframes disappear {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }

  @keyframes float {
    0% {
      transform: scale(1);
    }
    20% {
      transform: scale(1.05) rotateZ(5deg);
    }
    50% {
      transform: scale(0.9) rotateX(20deg);
    }
    100% {
      transform: rotateZ(-10deg);
    }
  }
</style>
