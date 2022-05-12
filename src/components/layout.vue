
<script setup>
  import { reactive } from 'vue'
  import Menu from './menu.vue'

  const data = reactive({
    menu: false
  })

  const toggleMenu = () => {
    data.menu = !data.menu
  }
</script>

<template>
  <div id="layout">
    <div class="sidebar">
      <div><!-- empty --></div>
      <div class="content" :class="{'-open': !data.menu}">
        <h1>Explore</h1>
        <div class="more-details">
          <button class="btn -more-details" @click="toggleMenu"></button>
          <span>More Details</span>
        </div>
      </div>
    </div>
    <Menu :isOpen='data.menu' @toggleMenu='toggleMenu'/>
  </div>
</template>

<style lang="scss" scoped>
  @import '../_colors';

  #layout {
    display: grid;
    grid: 1fr / 33.3% auto;
    height: 100vh;
    background: {
      image: url('/src/assets/Coding-Challenge-Image-Small-TinyPNG.png');
      size: cover;
    }
  }

  .btn {
    &.-more-details {
      color: var(--red);
      font: 36px/1 sans-serif;
      border-radius: 24px;
      width: 48px;
      height: 48px;
      background: #fff url('/src/assets/Plus.svg') center / 32px no-repeat;
    }
  }

  h1 {
    padding: 0 0 0 30%;
    font: 900 20vw/1 serif !important; // override bootstrap
    width: 0; // overflow trick
    margin: 0 0 -5%;
    animation: fadein 2000ms;
  }

  @keyframes fadein {
    from {
      opacity: 0;
      transform: translate(-15%, 0);
    }
    to {
      opacity: 1;
      transform: translate(0, 0);
    }
  }

  .content {
    opacity: 0;
    transition: opacity 250ms;
    color: #fff;

    &.-open {
      opacity: 1;
    }
  }

  .sidebar {
    display: grid;
    grid: 1fr auto / auto;
    background: var(--red);

    @media (min-width: 768px) {
      grid: 0.75fr auto / auto;
    }
  }

  .more-details {
    display: flex;
    gap: 18px;
    place-items: center;
    font-size: 24px;
    padding: 24px;

    @media (min-width: 768px) {
      place-content: flex-end;
    }

    > span {
      display: none;

      @media (min-width: 768px) {
        display: initial;
      }
    }
  }
</style>
