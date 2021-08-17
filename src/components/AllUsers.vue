<template>
  <div>
    <h1>Users</h1>
    <ul>
      <li v-for="user in users" v-bind:key="user.personId"><a :href="'/updateuser/'+user.personId">
        <div>User {{ user.lastName }} {{ user.firstName }}</div>
        </a>
        <input
          type="button"
          value="Löschen"
          v-on:click="deleteUser(user.personId)"
        />   
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "users",
  data() {
    return {
      users: [],
    };
  },
  created: async function () {
    this.updateData();
  },
  methods: {
    deleteUser: async function (id) {
      await axios.delete(`http://localhost:7071/api/user?id=${id}`);
      this.updateData();
    },
    updateData: async function () {
      let res = await axios.get("http://localhost:7071/api/user");
      this.users = res.data;
    },
  },
};
</script>

<style>
</style>

