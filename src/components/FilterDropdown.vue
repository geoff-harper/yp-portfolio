<template>
  <transition name="fade">
    <fieldset class="filter-category" v-show="filtersVisible">
      <h3 class="subtitle"><slot>Category</slot></h3>
      <div class="filter-option__container">
        <label v-for="category of Object.entries(displayFilters)" :key="category[0]" :for="category[0]" class="filter-option__label">
          <input
            class="filter-option__checkbox"
            :id="category[0]"
            type="checkbox"
            :value="category[0]"
            @change="emitFilters"
            v-model="checkedCategories">
          <span class="filter-option__span">{{ category[1] }}</span>
        </label>
      </div>
    </fieldset>
  </transition>
</template>

<script>
export default {
  name: 'FilterDropdown',
  model: {
    prop: 'checkedBoxes',
    event: 'change'
  },
  props: {
    checkedBoxes: {
      type: Array,
      required: true
    },
    displayFilters: {
      type: Object,
      required: true
    },
    idText: {
      type: String
    },
    filtersVisible: {
      type: Boolean
    }
  },
  methods: {
    emitFilters () {
      this.$emit('change', this.checkedCategories, this.idText)
    }
  },
  data () {
    return {
      checkedCategories: this.checkedBoxes
    }
  }
}
</script>
