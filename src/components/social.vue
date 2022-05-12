
<script setup>
</script>

<template>
  <div class="social">
    <a class='-fb' href="https://facebook.com" target="_blank"></a>
    <a class='-ig' href="https://instagram.com" target="_blank"></a>
  </div>
</template>

<style lang="scss" scoped>
  .social {
    display: grid;
    gap: 12px;
    place-content: flex-end;
    padding: 24px;
    white-space: nowrap;
    pointer-events: initial;

    @media (max-width: (768px - 1px)) {
      display: flex;
      place-items: flex-end;
    }
  }

  a {
    width: 48px;
    height: 48px;
    border-radius: 24px;
    background: #fff;

    &.-fb {
      mask: url('/src/assets/Facebook.svg');
      mask-position: center;
      mask-repeat: no-repeat;
      -webkit-mask: url('/src/assets/Facebook.svg');
      -webkit-mask-position: center;
      -webkit-mask-repeat: no-repeat;
    }

    &.-ig {
      mask: url('/src/assets/Instagram.svg');
      mask-position: center;
      mask-repeat: no-repeat;
      -webkit-mask: url('/src/assets/Instagram.svg');
      -webkit-mask-position: center;
      -webkit-mask-repeat: no-repeat;
    }
  }
</style>
