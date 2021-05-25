<template>
  <nav class="filter-nav">
      <!-- Send these values through updateFilter method to Home.vue-->
      <!-- databind a class of active IF the current filter is all.-->
      <button @click="updateFilter('all')" :class="{ active: current === 'all' }">View All</button>
      <!-- databind a class of active IF the current filter is completed-->
      <button @click="updateFilter('completed')" :class="{ active: current === 'completed' }">Completed</button>
      <!-- databind a class of active IF the current filter is ongoing -->
      <button @click="updateFilter('ongoing')" :class="{ active: current === 'ongoing' }">Ongoing</button>
  </nav>
</template>

<script>
export default {
    // accept the prop current
    props: ['current'],
    methods: {
        updateFilter(by) {
            this.$emit('filterChange', by)
        }
    }
}
</script>

<style>
.filter-nav button {
  background: rgb(32, 32, 32);
  padding: 15px;
  border: none;
  border-radius: 5px;
  color: rgb(221, 221, 221);
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button:hover {
  background: rgb(49, 49, 49);
  color: white;
}
.filter-nav button.active {
  border: 3px solid #00ce89;
  color: white;
}
.filters {
  text-align: center;
  margin: 50px 0 50px 0;
}
</style>