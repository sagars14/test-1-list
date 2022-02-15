<template>
  <table v-show="showTable" class="user-table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Created Date</th>
      </tr>
    </thead>
    <tbody v-for="(user, i) in usersList" :key="i">
      <tr>
        {{
          user.name
        }}
      </tr>
      <tr>
        {{
          formattedDate(user.created_at)
        }}
      </tr>
    </tbody>
  </table>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';
import moment from 'moment';

export default defineComponent({
  name: 'List',
  props: {
    usersList: {
      type: Array,
      required: true,
    },
    showTable: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    formattedDate(date) {
      return moment(date).fromNow();
    },
  },
});
</script>

<style lang="scss" scoped></style>
