<template>
  <form>
    <FilterDropdown
      @toggle=""
      :displayFilters="displayFilters.vertical"
      idText="vertical">Type of Business</FilterDropdown>
    <FilterDropdown
      :displayFilters="displayFilters.language"
      idText="language">Language</FilterDropdown>
    <FilterDropdown
      :displayFilters="displayFilters.features"
      idText="features">Website Features</FilterDropdown>
  </form>
</template>

<script>
import FilterDropdown from './FilterDropdown'

export default {
  name: 'SearchFilters',
  components: { FilterDropdown },
  data () {
    return {
      displayFilters: {
        vertical: ['Automotive', 'Commercial and Industrial Services', 'Contractors and Construction', 'Food Services', 'Health, Beauty and Well-Being', 'Home and Maintenance', 'Law and Finance', 'Miscellaneous'],
        language: ['English', 'French', 'Bilingual'],
        features: ['Blog', 'Catalogue', 'Video Background', 'Parallax Images']
      },
      activeFilters: {
        vertical: [],
        language: [],
        features: []
      }
    }
  },
  methods: {
    emitFilters () {

    }
  }

}
</script>

<style>

</style>
