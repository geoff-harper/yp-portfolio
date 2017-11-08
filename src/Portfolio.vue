<template>
  <main id='portfolio'>
    <section class="filter-section">
      <form>
        <FilterDropdown
          v-model="updateSites"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.vertical"
          idText="vertical">Type of Business</FilterDropdown>
        <FilterDropdown
          v-model="updateSites"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.language"
          idText="language">Language</FilterDropdown>
        <FilterDropdown
          v-model="updateSites"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.features"
          idText="features">Website Features</FilterDropdown>
        <FilterDropdown
          v-model="updateSites"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.colour"
          idText="colour">Colour</FilterDropdown>
      </form>
      <div class="filter-buttons__container">
        <button class="filter-toggle" @click="filtersVisible = !filtersVisible">{{ filtersVisible ? "Hide" : "Show" }} filters</button>
        <button class="filter-reset" @click="clearFilters">Reset filters</button>
      </div>
    </section>
    <section class="results-section">
      <SitesList :portfolios="portfolios" :activeFilters="activeFilters"></SitesList>
    </section>
  </main>
</template>

<script>
import FilterDropdown from './components/FilterDropdown'
import SitesList from './components/SitesList'

let currentPortfolioId = 0

export default {
  name: 'portfolio',
  components: {
    FilterDropdown,
    SitesList
  },
  methods: {
    updateSites (sites, category) {
      this.activeFilters[category] = sites
    },
    clearFilters () {
      this.activeFilters = {
        vertical: [],
        language: [],
        features: [],
        colour: []
      }
    }
  },
  data () {
    return {
      portfolios: [
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 1',
          imageFile: 'port1.jpg',
          link: '#',
          vertical: 'Automotive',
          specialty: 'Towing',
          language: 'English',
          features: ['Video Background'],
          colour: 'Green'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 2',
          imageFile: 'port2.jpg',
          link: '#',
          vertical: 'Health, Beauty and Well-Being',
          specialty: 'Denturist',
          language: 'English',
          features: ['Blog', 'Video Background'],
          colour: 'Blue'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 3',
          imageFile: 'port3.jpg',
          link: '#',
          vertical: 'Contractors and Construction',
          specialty: 'Cabinets',
          language: 'Bilingual',
          features: ['Catalogue', 'Parallax Images'],
          colour: 'Multicoloured'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 4',
          imageFile: 'port4.jpg',
          link: '#',
          vertical: 'Health, Beauty and Well-Being',
          specialty: 'Dentist',
          language: 'French',
          features: [],
          colour: 'Red'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 5',
          imageFile: 'port5.jpg',
          link: '#',
          vertical: 'Home and Maintenance',
          specialty: 'Carpet Cleaning',
          language: 'English',
          features: ['Mockup', 'Parallax Images'],
          colour: 'Yellow'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 6',
          imageFile: 'port6.jpg',
          link: '#',
          vertical: 'Health, Beauty and Well-Being',
          specialty: 'Spa',
          language: 'English',
          features: ['Mockup'],
          colour: 'Green'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 7',
          imageFile: 'port7.jpg',
          link: '#',
          vertical: 'Food Services',
          specialty: 'Banquet Hall',
          language: 'English',
          features: ['Parallax Images'],
          colour: 'Black and White'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 8',
          imageFile: 'port8.jpg',
          link: '#',
          vertical: 'Miscellaneous',
          specialty: 'Daycare',
          language: 'French',
          features: ['Blog', 'Parallax Images'],
          colour: 'Multicoloured'
        }
      ],
      displayFilters: {
        vertical: ['Automotive', 'Commercial and Industrial Services', 'Contractors and Construction', 'Food Services', 'Health, Beauty and Well-Being', 'Home and Maintenance', 'Law and Finance', 'Miscellaneous'],
        language: ['English', 'French', 'Bilingual'],
        features: ['Blog', 'Catalogue', 'Video Background', 'Parallax Images', 'Mockup'],
        colour: ['Red', 'Green', 'Blue', 'Yellow', 'Purple', 'Orange', 'Pink', 'Black and White', 'Multicoloured']
      },
      activeFilters: {
        vertical: [],
        language: [],
        features: [],
        colour: []
      },
      filtersVisible: true
    }
  }
}
</script>

<style>
</style>
