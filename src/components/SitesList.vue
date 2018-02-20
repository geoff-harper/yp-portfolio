<template>
  <transition-group name="site-example" tag="ul" class="results-list">
    <SiteExample
      v-for="(portfolio, i) of filteredSites"
      :key="portfolio.id"
      :subVertical="getSubVertical(portfolio)"
      :portfolio="portfolio">
    </SiteExample>
    <li class="no-results" v-if="filteredSites.length === 0" :key="9999">{{ resultsData }}</li>
  </transition-group>
</template>

<script>
import SiteExample from './SiteExample'
import { filterData, resultsData } from '../assets/textTranslations'

export default {
  name: 'SitesList',
  components: { SiteExample },
  props: {
    portfolios: { type: Array, required: true },
    activeFilters: { type: Object, required: true },
    lang: { type: String, required: true }
  },
  methods: {
    getSubVertical (portfolio) {
      return this.verticalData[portfolio.verticals]['subVerticals'][portfolio.specialty]
    }
  },
  computed: {
    filteredSites () {
      // Filter categories
      const filters = Object.keys(this.activeFilters)
      // All portfolio examples
      let newSites = this.portfolios
      // Checked filter options
      let filterCounter = 0

      // Collect # of checked filter options
      for (let _filter of filters) {
        filterCounter += this.activeFilters[_filter].length
      }

      if (filterCounter !== 0) {
        // Sites to appear
        newSites = newSites.filter(portfolio => {
          let truthy = true
          // For each filter cateogry
          for (let _filter of filters) {
            // If any filter options selected in this category
            if (this.activeFilters[_filter].length !== 0) {
              // If portfolio prop is a string else array
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
  },
  data () {
    return {
      resultsData: resultsData[this.lang],
      verticalData: filterData.verticals[this.lang]
    }
  }
}
</script>
