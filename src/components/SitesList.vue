<template>
  <!-- <ul class="results-list"> -->
  <transition-group name="site-example" tag="ul" class="results-list">
    <Site
      v-for="portfolio of filteredSites"
      :key="portfolio.id"
      :portfolio="portfolio"
    ></Site>
  </transition-group>
  <!-- </ul> -->
</template>

<script>
import Site from './SiteExample'

export default {
  name: 'SitesList',
  components: { Site },
  props: {
    portfolios: {
      type: Array,
      required: true
    },
    activeFilters: {
      type: Object,
      required: true
    }
  },
  data () {
    return {

    }
  },
  computed: {
    filteredSites () {
      let newSites = this.portfolios
      const filters = Object.keys(this.activeFilters)
      let filterCounter = 0

      for (let _filter of filters) { filterCounter += this.activeFilters[_filter].length }

      if (filterCounter !== 0) {
        newSites = newSites.filter(portfolio => {
          let truthy = true
          for (let _filter of filters) {
            if (this.activeFilters[_filter].length !== 0) {
              if (typeof portfolio[_filter] === 'string') {
                truthy = this.activeFilters[_filter].indexOf(portfolio[_filter]) !== -1 && truthy
              } else if (Array.isArray(portfolio[_filter])) {
                truthy = portfolio[_filter].some(r => this.activeFilters[_filter].indexOf(r) !== -1) && truthy
              }
            }
          }
          return truthy
        })
      }
      return newSites
    }
  }
}
</script>

<style>

</style>
