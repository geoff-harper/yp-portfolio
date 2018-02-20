<template>
  <li class="site-example">
    <a :href="portfolio.link" target="_blank" rel="noopener">
      <img :src="fullPath" :alt="portfolio.name" class="portfolio-image">
      <p class="smallsubtitle">{{ subVertical }}</p>
      <p class="bodytext">{{ getExampleId(portfolio.id, 3) }}</p>
      <!-- <div class="mockup-identifier" v-if="portfolio.features.indexOf('Mockup') !== -1">Mockup</div> -->
    </a>
  </li>
</template>

<script>
export default {
  name: 'SiteExample',
  props: {
    portfolio: { type: Object, required: true },
    subVertical: { type: String, required: true }
  },
  computed: {
    fullPath () {
      return `/uploads/${this.portfolio.imageFile}`
    }
  },
  methods: {
    getExampleId (num, numZeros) {
      const n = Math.abs(num)
      const zeros = Math.max(0, numZeros - Math.floor(n).toString().length)
      const zeroString = Math.pow(10, zeros).toString().substr(1)
      return '#' + zeroString + n
    }
  },
  data () {
    return {}
  }
}
</script>

<style>

</style>
