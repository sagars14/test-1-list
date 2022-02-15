<template>
  <div class="main-container">
    <SearchBar @find="findUser($event)" />
    <p v-show="showMatchFound" style="text-align: center; width: 700px">
      <span><strong>Match Found!</strong></span>
    </p>
    <div class="user-list">
      <div class="left-section">
        <List :usersList="users" />
      </div>
      <div class="right-section">
          
      </div>
    </div>
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
      tempUsers: [],
      tempFlag: true,
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
    findUser(uname) {
      if (this.users && this.users.length > 0) {
        const foundedUser = this.users.find(
          (user) => user.name.toLowerCase() === uname.toLowerCase()
        );
        if (foundedUser && foundedUser !== undefined) {
          if (this.tempFlag) this.tempUsers = [...this.users];
          this.users = [foundedUser];
          this.tempFlag = false;
        }
      }

      if (!uname && uname === '') {
        this.users = [...this.tempUsers];
      }
    },
  },
});
</script>

<style lang="scss" scoped></style>
