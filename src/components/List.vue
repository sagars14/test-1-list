<template>
  <table class="user-table">
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
          user.created_at
        }}
      </tr>
    </tbody>
  </table>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';

export default defineComponent({
  name: 'List',
  props: {
    usersList: {
      type: Array,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped></style>
