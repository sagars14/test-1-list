<template>
  <div class="search-bar">
    <input v-model="searchValue" placeholder="Search or Add..." type="search" />
  </div>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';

export default defineComponent({
  name: 'SearchBar',
  data() {
    return {
      searchValue: '',
    };
  },
  watch: {
    searchValue() {
      this.$emit('find', this.searchValue);
    },
  },
});
</script>

<style lang="scss" scoped></style>
