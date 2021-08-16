<template>
  <div>
      <h1>Users</h1>
      <ul>
          <li v-for="user in users" v-bind:key="user.personID">{{user.lastName}} {{user.firstName}}</li>
      </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'users',
    data() {
        return{
            users: []
        }
    },
    created: async function(){
        let res = await axios.get("http://localhost:7071/api/user")
        this.users = res.data
    }
}
</script>

<style>

</style>

