<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{active: currentFilter == 'all'}" >View All</button>
    <button @click="updateFilter('completed')" :class="{active: currentFilter == 'completed'}" >Completed</button>
    <button @click="updateFilter('onGoing')" :class="{active: currentFilter == 'onGoing'}" >On Going</button>
  </nav>
</template>

<script>
export default {
  props: ['currentFilter'],
  methods: {
    updateFilter (filterBy) {
      this.$emit('filterChange', filterBy)
    }
  }
}
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
