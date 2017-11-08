<template>
  <fieldset class="filter-category">
    <h3 class="subtitle"><slot>Category</slot></h3>
    <transition name="shrink">
      <div class="filter-option__container" v-show="filtersVisible">
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
    </transition>
  </fieldset>
</template>

<script>
export default {
  name: 'FilterDropdown',
  props: {
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
      this.$emit('toggle', this.checkedCategories, this.idText)
    },
    getId (i) {
      return `${this.idText}-${i}`
    }
  },
  computed: {

  },
  data () {
    return {
      checkedCategories: []
    }
  }
}
</script>

<style>

</style>
