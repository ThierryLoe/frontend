<template>
  <div>
    <div>User {{ $route.params.id }}</div>
    <div class="about" v-if="user != null">
      <input type="text" placeholder="Vorname" v-model="user.firstName" />
      <input type="text" placeholder="Nachname" v-model="user.lastName" />
      <input
        type="submit"
        value="Save"
        v-on:click="update()"
        
        
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "updateuser",
  data() {
    return {
      user: null,
    };
  },
  created: async function () {
    this.oneUser();
  },
  methods: {
    oneUser: async function () {
      let res = await axios.get(
        `http://localhost:7071/api/user/${this.$route.params.id}`
      );
      this.user = res.data;
    },
    update: async function () {
      if (this.firstName != "" && this.lastName != "") {
        await axios.put(
          `http://localhost:7071/api/user/${this.user.personId}?firstname=${this.user.firstName}&lastname=${this.user.lastName}`
        );
      }
      this.$router.push('/')
    },
  },
  computed: {
    checkInputs: function () {
      return this.user.firstName != "" && this.user.lastName != "";
    },
  },
};
</script>

<style>
</style>