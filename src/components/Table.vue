<template>
  <div class="main-container">
    <SearchBar @find="findUser($event)" />
    <List :usersList="users" />
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
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    const usersData = [
      { name: 'Ashish', created_at: new Date() },
      { name: 'Rahul', created_at: new Date() },
      { name: 'Aanand', created_at: new Date() },
      { name: 'Rahul', created_at: new Date() },
      { name: 'Ravi', created_at: new Date() },
      { name: 'Pushark', created_at: new Date() },
      { name: 'Shubham', created_at: new Date() },
      { name: 'Ankit', created_at: new Date() },
      { name: 'Kuldeep', created_at: new Date() },
    ];
    window.localStorage.setItem('users', JSON.stringify(usersData));
    window.localStorage.getItem('users');
    this.users = [...usersData];
  },
  methods: {
    //   findUser() {

    //   }
  }
});
</script>

<style lang="scss" scoped></style>
