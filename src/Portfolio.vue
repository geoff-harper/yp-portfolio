<template>
  <main id='portfolio'>
    <section class="filter-section">
      <form>
        <FilterDropdown
          v-model="activeFilters.vertical"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.vertical"
          idText="vertical">Type of Business</FilterDropdown>
        <FilterDropdown
          v-model="activeFilters.language"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.language"
          idText="language">Language</FilterDropdown>
        <FilterDropdown
          v-model="activeFilters.features"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.features"
          idText="features">Website Features</FilterDropdown>
      </form>
      <div class="filter-buttons__container">
        <button :class="['filter-toggle', filtersVisible ? 'expanded' : null]" @click="filtersVisible = !filtersVisible">
          <!-- <img src="/uploads/toggle.png" alt="toggle icon" class="filter-toggle__icon"> -->
          {{ filtersVisible ? "Hide" : "Show" }} filters
        </button>
        <button class="filter-reset" @click="resetFilters">
          <!-- <img src="/uploads/reset.png" alt="reset icon" class="filter-toggle__icon"> -->
          Reset filters
        </button>
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
import TextTranslations from './assets/textTranslations'

let currentPortfolioId = 0

export default {
  name: 'Portfolio',
  components: {
    FilterDropdown,
    SitesList
  },
  methods: {
    updateSites (sites, category) {
      this.activeFilters[category] = sites
    },
    resetFilters () {
      this.activeFilters = {
        vertical: [],
        language: [],
        features: []
      }
    },
    shufflePortfolios () {
      let array = this.portfolios
      let currentIndex = array.length
      let temporaryValue
      let randomIndex

      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex)
        currentIndex -= 1

        temporaryValue = array[currentIndex]
        array[currentIndex] = array[randomIndex]
        array[randomIndex] = temporaryValue
      }

      this.portfolios = array
    },
    getLang () {
      return document.documentElement.getAttribute('lang')
    },
    setFilterMaps (arr) {
      const _map = new Map(arr.verticals)
      _map.forEach((value, key) => {
        value.subVerticals = new Map(value.subVerticals)
      })
      this.filters['verticals'] = _map
      this.filters['language'] = new Map(arr.language)
      this.filters['features'] = new Map(arr.features)
    }
  },
  created () {
    this.shufflePortfolios()
  },
  mounted () {
    this.setFilterMaps(TextTranslations.filters)
  },
  data () {
    return {
      portfolios: [
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 1',
          imageFile: 'site1.jpg',
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
          imageFile: 'site2.jpg',
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
          imageFile: 'site3.jpg',
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
          imageFile: 'site4.jpg',
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
          imageFile: 'site5.jpg',
          link: '#',
          vertical: 'Home and Maintenance',
          specialty: 'Carpet Cleaning',
          language: 'English',
          features: ['Parallax Images'],
          colour: 'Yellow'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 6',
          imageFile: 'site6.jpg',
          link: '#',
          vertical: 'Health, Beauty and Well-Being',
          specialty: 'Spa',
          language: 'English',
          features: [],
          colour: 'Green'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 7',
          imageFile: 'site7.jpg',
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
          imageFile: 'site8.jpg',
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
        features: ['Blog', 'Catalogue', 'Video Background', 'Parallax Images']
      },
      activeFilters: {
        vertical: [],
        language: [],
        features: []
      },
      filters: {
        verticals: [],
        language: [],
        features: []
      },
      filterTitles: TextTranslations.filters.titles[this.getLang()],
      buttonText: TextTranslations.buttons[this.getLang()],
      filtersVisible: true
    }
  }
}
</script>
