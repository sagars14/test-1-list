<template>
  <div class="main-container">
    <SearchBar
      :show-add-btn="showAddBtn"
      @find="findUser($event)"
      @add="addUser($event)" />
    <p v-show="showMatchFound" style="text-align: center; width: 700px">
      <span><strong>Match Found!</strong></span>
    </p>
    <div class="user-list">
      <div class="left-section">
        <List
          :showTable="showTable"
          :usersList="users"
          @delete="deleteUser($event)" />
      </div>
      <div class="right-section"></div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';
import SearchBar from './SearchBar.vue';
import List from './List.vue';
import moment from 'moment';

export default defineComponent({
  name: 'Table',
  components: {
    SearchBar,
    List,
  },
  data() {
    return {
      showTable: true,
      tempFlag: true,
      showAddBtn: false,
      showMatchFound: false,
      users: [],
      tempUsers: [],
    };
  },
  mounted() {
    const usersData = [
      {
        name: 'Ashish',
        created_at: moment(moment(new Date().toString()).day(-7)),
      },
      { name: 'Rahul', created_at: moment(new Date().toString()).day(-7) },
      { name: 'Aanand', created_at: moment(new Date().toString()).day(-6) },
      { name: 'Rahul', created_at: moment(new Date().toString()).day(-5) },
      { name: 'Ravi', created_at: moment(new Date().toString()).day(-4) },
      { name: 'Pushark', created_at: moment(new Date().toString()).day(-3) },
      { name: 'Shubham', created_at: moment(new Date().toString()).day(-2) },
      { name: 'Ankit', created_at: moment(new Date().toString()).day(-1) },
      { name: 'Kuldeep', created_at: moment(new Date().toString()).day(0) },
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
          this.showTable = true;
          this.showAddBtn = false;
          this.tempFlag = false;
          this.showMatchFound = true;
        } else {
          this.showMatchFound = false;
          this.showAddBtn = true;
          this.showTable = false;
        }
      }

      if (!uname && uname === '') {
        if (this.tempUsers.length > 0) this.users = [...this.tempUsers];
        this.showTable = true;
        this.showAddBtn = false;
      }
    },
    addUser(newUser) {
      if (newUser && newUser !== '') {
        this.users.unshift({
          name: newUser,
          created_at: moment(new Date()),
        });
        this.showAddBtn = false;
        this.showTable = true;
        this.tempUsers = [...this.users];
        window.localStorage.removeItem('users');
        window.localStorage.setItem('users', JSON.stringify([...this.users]));
      }
    },
    deleteUser(name) {
      const filteredUsers = this.users.filter(
        (user) => user.name.toLowerCase() !== name.toLowerCase()
      );
      this.users = [...filteredUsers];
      this.tempUsers = [...filteredUsers];
      window.localStorage.removeItem('users');
      window.localStorage.setItem('users', JSON.stringify([this.users]));
    },
  },
});
</script>

<style lang="scss" scoped></style>
