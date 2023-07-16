<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <FooterApp></FooterApp>
</template>
<script>
// @ is an alias to /src
import FooterApp from '@/components/Footer.vue'

export default {
  name: 'AboutView',
  components: {
    FooterApp
  }
  }
</script>