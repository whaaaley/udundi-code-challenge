
<script setup>
</script>

<template>
  <div id="explore">
    <h1>Explore</h1>
    <hr/>
    <p>
Sed ut perspiciatis unde omnis iste natus error sit voluptatem
accusantium doloremque laudantium, totam rem aperiam, eaque
ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae
dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas
sit aspernatur aut odit aut fugit, sed quia consequuntur magni
dolores eos qui ratione voluptatem sequi nesciunt. Neque porro
quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur,
adipisci velit, sed quia non numquam eius modi tempora incidunt ut
labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad
minima veniam, quis nostrum exercitationem ullam corporis suscipit
laboriosam, nisi ut aliquid ex ea commodi consequatur?
    </p>
    <div class="d-flex justify-content-left">
      <button class="btn -read-more">Read More</button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  @import '../_colors';

  h1 {
    font: 600 calc(3rem + 1.5vw)/1 serif;
    color: var(--red);
  }

  hr {
    height: 2px !important; // override boostrap
    opacity: initial;
    background: linear-gradient(90deg, var(--red), transparent);
  }

  .btn {
    &.-read-more {
      text-transform: uppercase;
      font: 21px/1 sans-serif;
      padding: 21px 36px;
      color: #fff;
      border-radius: initial; // override bootstrap
      background: linear-gradient(90deg, $red, rgba($red, 0.75));
    }
  }
</style>
