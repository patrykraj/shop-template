<template>
  <div
    :class="sorting ? 'section-header-wrapper sort' : 'section-header-wrapper'"
  >
    <h2
      :class="showFilter ? 'filter-btn' : null"
      @click="handleSetFiltersActive"
    >
      {{ title }}
    </h2>
    <FilterButton
      v-if="showFilter"
      :filtersActive="filtersActive"
      :setFiltersActive="setFiltersActive"
    />
    <Sort v-if="sorting" />
  </div>
</template>

<script>
import Sort from "../products/Sort.vue";
import FilterButton from "./FilterButton.vue";

export default {
  name: "SectionHeader",
  props: {
    title: String,
    sorting: Boolean,
    showFilter: Boolean,
    filtersActive: Boolean,
    setFiltersActive: Function,
  },
  components: {
    Sort,
    FilterButton,
  },
  methods: {
    handleSetFiltersActive() {
      this.setFiltersActive();
    },
  },
};
</script>

<style scoped>
div.section-header-wrapper {
  border-bottom: 3px solid #2c3e50;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

h2 {
  text-align: left;
  font-size: 2rem;
  margin: 10px 0;
}

h2.filter-btn {
  cursor: pointer;
}

@media (max-width: 500px) {
  div.section-header-wrapper.sort {
    flex-flow: column;
  }
}
</style>
