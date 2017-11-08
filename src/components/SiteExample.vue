<template>
  <li class="site-example">
    <!-- <a :href="portfolio.link" target="_blank"> -->
      <!-- <img :src="fullPath" :alt="portfolio.name" class="portfolio-image"> -->
      <h3 class="smallsubtitle">{{ portfolio.name }}</h3>
      <p class="bodytext">{{ portfolio.vertical }}</p>
      <p class="bodytext">{{ portfolio.specialty }}</p>
      <p class="bodytext">{{ portfolio.features }}</p>
      <p class="bodytext">{{ portfolio.colour }}</p>
      <p class="bodytext">{{ portfolio.language }}</p>
    <!-- </a> -->
  </li>
</template>

<script>
export default {
  name: 'Site',
  props: {
    portfolio: {
      type: Object,
      required: true
    }
  },
  data () {
    return {

    }
  },
  computed: {
    fullPath () {
      return `/uploads/${this.portfolio.imageFile}`
    }
  }
}
</script>

<style>

</style>
