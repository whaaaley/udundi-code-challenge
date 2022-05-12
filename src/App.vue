<script setup>
  import Layout from './components/layout.vue'
</script>

<template>
  <Layout>
    <h1>hello</h1>
  </Layout>
</template>

<style lang='scss'>
  @import './_bootstrap';
  @import './_colors';

  :root {
    --red: #{$red};
  }
</style>
