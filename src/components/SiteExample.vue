<template>
  <li class="site-example">
    <a :href="portfolio.link" target="_blank" rel="noopener">
      <!-- <img :src="fullPath" :alt="portfolio.name" class="portfolio-image"> -->
      <!-- <h3 class="smallsubtitle">{{ portfolio.name }}</h3> -->
      <!-- <p class="bodytext">{{ portfolio.vertical }}</p> -->
      <p class="smallsubtitle">{{ portfolio.specialty }}</p>
      <p class="bodytext">{{ getExampleId(portfolio.id, 3) }}</p>
      <!-- <p class="bodytext">{{ portfolio.features }}</p> -->
      <!-- <p class="bodytext">{{ portfolio.colour }}</p> -->
      <!-- <p class="bodytext">{{ portfolio.language }}</p> -->
      <!-- <div class="mockup-identifier" v-if="portfolio.features.indexOf('Mockup') !== -1">Mockup</div> -->
    </a>
  </li>
</template>

<script>
export default {
  name: 'SiteExample',
  props: {
    portfolio: {
      type: Object,
      required: true
    }
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
