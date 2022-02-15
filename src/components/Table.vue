<template>
  <div class="main-container">
    <SearchBar />
    <List />
  </div>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';
import SearchBar from './SearchBar.vue';
import List from './List.vue';

export default defineComponent({
  name: 'Table',
  components: {
    SearchBar,
    List,
  },
});
</script>

<style lang="scss" scoped></style>
