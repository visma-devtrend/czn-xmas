<template>
  <div class="greeting">
    <div class="snow-area">
      <div class="snow snow--near"></div>
      <div class="snow snow--near snow--alt"></div>

      <div class="snow snow--mid"></div>
      <div class="snow snow--mid snow--alt"></div>

      <div class="snow snow--far"></div>
      <div class="snow snow--far snow--alt"></div>
    </div>

    <h2>Greetings from development team in Vilnius!</h2>
    <img src="../assets/raudonikiai.jpg" alt="" style="width: 100%">
    <p>
      2018 has been an exciting year with you.
      We have built cool stuff that is going to be used daily by our ever-growing customer base.
      Let's see what the Year of the Pig brings to our lives in 2019. Fingers crossed!
    </p>
    <h3>Merry Christmas and a Happy New Year!</h3>
    <img src="../assets/nerd-pig.gif">
  </div>
</template>

<script lang="ts">

  import { Component, Vue } from 'vue-property-decorator';

  @Component
  export default class Greeting extends Vue {

  }
</script>

<style lang="scss">
  $s--near: 10s;
  $s--mid: ($s--near * 2);
  $s--far: ($s--near * 3);

  $ease--out-quad: cubic-bezier(.25,.46,.450,.94);

  .greeting {
    overflow: hidden;
  }

  .snow-area {
    position: absolute;
    overflow: hidden;
    height: 100vh;
    width: 100vw;
    top: 0;
    left: 0;
  }

  %on-top {
    z-index: 100;
    pointer-events: none;
  }

  .snow {
    @extend %on-top;
    position: absolute;
    top: 0; right: 0; bottom: 0; left: 0;
    animation: falling linear infinite both;
    transform: translate3D(0,-100%,0);

    &--near {
      animation-duration: $s--near;
      background-image: url('https://dl6rt3mwcjzxg.cloudfront.net/assets/snow/snow-large-075d267ecbc42e3564c8ed43516dd557.png');
      background-size: contain;

      & + .snow--alt {
        animation-delay: ($s--near / 2);
      }
    }

    &--mid {
      animation-duration: $s--mid;
      background-image: url('https://dl6rt3mwcjzxg.cloudfront.net/assets/snow/snow-medium-0b8a5e0732315b68e1f54185be7a1ad9.png');
      background-size: contain;

      & + .snow--alt {
        animation-delay: ($s--mid / 2);
      }
    }

    &--far {
      animation-duration: $s--far;
      background-image: url('https://dl6rt3mwcjzxg.cloudfront.net/assets/snow/snow-small-1ecd03b1fce08c24e064ff8c0a72c519.png');
      background-size: contain;

      & + .snow--alt {
        animation-delay: ($s--far / 2);
      }
    }
  }

  @keyframes falling {
    0% {
      transform: translate3D(-7.5%,-100%, 0);
    }

    100% {
      transform: translate3D(7.5%,100%, 0);
    }
  }
</style>
