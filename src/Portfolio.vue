<template>
  <main id='portfolio'>
    <section class="filter-section">
      <form>
        <FilterDropdown
          v-model="activeFilters.verticals"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.verticals"
          idText="verticals">Type of Business</FilterDropdown>
        <FilterDropdown
          v-model="activeFilters.languages"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.languages"
          idText="languages">Language</FilterDropdown>
        <FilterDropdown
          v-model="activeFilters.features"
          :filtersVisible="filtersVisible"
          :displayFilters="displayFilters.features"
          idText="features">Website Features</FilterDropdown>
      </form>
      <div class="filter-buttons__container">
        <button :class="['filter-toggle', filtersVisible ? 'expanded' : null]" @click="filtersVisible = !filtersVisible">
          <!-- <img src="/uploads/toggle.png" alt="toggle icon" class="filter-toggle__icon"> -->
          {{ filtersVisible ? buttonText.hide : buttonText.show }}
        </button>
        <button class="filter-reset" @click="resetFilters">
          <!-- <img src="/uploads/reset.png" alt="reset icon" class="filter-toggle__icon"> -->
          {{ buttonText.reset }}
        </button>
      </div>
    </section>
    <section class="results-section">
      <SitesList
        :lang="getLang()"
        :portfolios="portfolios"
        :activeFilters="activeFilters"></SitesList>
    </section>
  </main>
</template>

<script>
import FilterDropdown from './components/FilterDropdown'
import SitesList from './components/SitesList'
import { filterData, buttonData } from './assets/textTranslations'

let currentPortfolioId = 0

export default {
  name: 'Portfolio',
  components: {
    FilterDropdown,
    SitesList
  },
  methods: {
    resetFilters () {
      this.activeFilters = {
        verticals: [],
        languages: [],
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
    getFilterStrings (obj) {
      let newObj = {}
      Object.keys(obj).forEach(prop => {
        newObj[prop] = obj[prop].label || obj[prop]
      })
      return newObj
    }
  },
  created () {
    this.shufflePortfolios()
  },
  data () {
    return {
      portfolios: [
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 1',
          imageFile: 'site1.jpg',
          link: '#',
          verticals: 'auto',
          specialty: 'auto_8',
          languages: 'english',
          features: ['videoBackground'],
          colour: 'Green'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 2',
          imageFile: 'site2.jpg',
          link: '#',
          verticals: 'health',
          specialty: 'health_4',
          languages: 'english',
          features: ['blog', 'videoBackground'],
          colour: 'Blue'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 3',
          imageFile: 'site3.jpg',
          link: '#',
          verticals: 'construction',
          specialty: 'construction_5',
          languages: 'bilingual',
          features: ['catalogue', 'parallax'],
          colour: 'Multicoloured'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 4',
          imageFile: 'site4.jpg',
          link: '#',
          verticals: 'health',
          specialty: 'health_3',
          languages: 'french',
          features: [],
          colour: 'Red'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 5',
          imageFile: 'site5.jpg',
          link: '#',
          verticals: 'home',
          specialty: 'home_28',
          languages: 'english',
          features: ['parallax'],
          colour: 'Yellow'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 6',
          imageFile: 'site6.jpg',
          link: '#',
          verticals: 'health',
          specialty: 'health_13',
          languages: 'english',
          features: [],
          colour: 'Green'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 7',
          imageFile: 'site7.jpg',
          link: '#',
          verticals: 'food',
          specialty: 'food_2',
          languages: 'english',
          features: ['parallax'],
          colour: 'Black and White'
        },
        {
          id: ++currentPortfolioId,
          name: 'Portfolio Site 8',
          imageFile: 'site8.jpg',
          link: '#',
          verticals: 'misc',
          specialty: 'misc_1',
          languages: 'french',
          features: ['blog', 'parallax'],
          colour: 'Multicoloured'
        }
      ],
      activeFilters: {
        verticals: [],
        languages: [],
        features: []
      },
      displayFilters: {
        verticals: this.getFilterStrings(filterData.verticals[this.getLang()]),
        languages: this.getFilterStrings(filterData.languages[this.getLang()]),
        features: this.getFilterStrings(filterData.features[this.getLang()])
      },
      filterTitles: filterData.titles[this.getLang()],
      buttonText: buttonData[this.getLang()],
      filtersVisible: true
    }
  }
}
</script>
