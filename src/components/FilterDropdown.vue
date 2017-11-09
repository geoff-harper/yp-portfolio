<template>
  <transition name="fade">
    <fieldset class="filter-category" v-show="filtersVisible">
      <h3 class="subtitle"><slot>Category</slot></h3>
      <div class="filter-option__container">
        <label v-for="(category, i) of displayFilters" key="i" :for="getId(i)" class="filter-option__label">
          <input
            class="filter-option__checkbox"
            :id="getId(i)"
            type="checkbox"
            :value="category"
            @change="emitFilters"
            v-model="checkedCategories">
          {{ category }}
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
      type: Array,
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
    },
    getId (i) {
      return `${this.idText}-${i}`
    }
  },
  watch: {
    checkedBoxes () {
      this.checkedCategories = this.checkedBoxes
    }
  },
  data () {
    return {
      checkedCategories: this.checkedBoxes
    }
  }
}
</script>

<style>

</style>
