
<script setup>
  import { ref, reactive, defineProps, onMounted } from 'vue'

  import Social from './social.vue'
  import Article from './article.vue'

  const props = defineProps({
    isOpen: Boolean,
    origin: Array,
  })

  const data = reactive({
    top: 0,
    left: 0
  })

  const contentRef = ref(null)

  const updatePosition = () => {
    const el = contentRef.value
    const cs = getComputedStyle(el)

    const paddingX = parseFloat(cs.paddingLeft);
    const paddingY = parseFloat(cs.paddingTop);

    const contentRect = el.getBoundingClientRect()

    data.top = contentRect.y + paddingY
    data.left = contentRect.x + paddingX
  }

  onMounted(() => {
    updatePosition()
  })

  addEventListener('resize', () => {
    updatePosition()
  })
</script>

<template>
  <div class="layer" :class="{'-click-through': !props.isOpen}">
    <div class="side" :class="{'-open': props.isOpen}"><!-- empty --></div>
    <div class="content" ref="contentRef">
      <div
        class="box"
        :class="{'-open': props.isOpen}"
        :style="{
          '--x': props.origin[0] - data.left + 'px',
          '--y': props.origin[1] - data.top + 'px'
        }"
      >
        <button class="-close" @click="$emit('closeMenu')">×</button>
        <div class="inner" :class="{'-open': props.isOpen}">
          <!-- v-if to prevent content from overflowing when visibly hidden -->
          <!-- we can't v-if higher in the doc without breaking transitions -->
          <Article v-if="props.isOpen"/>
        </div>
      </div>
    </div>
    <Social/>
  </div>
</template>

<style lang="scss" scoped>
  @import '../_colors';

  .layer {
    display: grid;
    grid: auto / 0 1fr auto;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    &.-click-through {
      pointer-events: none;
    }

    @media (min-width: 768px) {
      grid: auto / 96px 1fr 0.25fr;
    }

    @media (min-width: (1024px - 1px)) {
      grid: auto / 96px 1fr 0.5fr;
    }

    @media (min-width: (1440px - 1px)) {
      grid: auto / 96px 1fr 1fr;
    }
  }

  .side {
    background: rgba(#000, 0.25);
    transform: translate(-100%, 0);
    transition: 200ms transform;

    &.-open {
      transform: translate(0, 0);
    }
  }

  .content {
    display: grid;
    transition: padding 200ms;
    z-index: 1;

    @media (min-width: 768px) {
      padding: {
        top: 96px + 24px;
        bottom: 96px;
      }
    }
  }

  .box {
    background: #fff;
    padding: min(max(24px, 5vw), 64px);
    color: transparent;
    line-height: 2;
    transform-origin: var(--x) var(--y);
    transition: transform 250ms;
    transform: scale(0);
    box-shadow: 0 12px 24px rgb(#000, 0.5);

    &.-open {
      color: initial;
      transform: scale(1);

      // mobile only
      @media (max-width: (768px - 1px)) {
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        min-height: 100vh;
      }
    }

    button {
      &.-close {
        position: absolute;
        border: initial; // override bootstrap
        background: initial; // override browser
        top: 0;
        right: 0;
        width: 48px;
        height: 48px;
        color: var(--red);
        font: 36px/48px sans-serif;
      }
    }
  }

  .inner {
    opacity: 0;
    transform: translate(-36px, 0);
    transition:
      500ms transform 250ms,
      500ms opacity 250ms + 100ms;

    &.-open {
      transform: translate(0, 0);
      opacity: 1;
    }
  }
</style>
