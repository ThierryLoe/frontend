<template>
  <div class="about">
    <input type="text" placeholder="Vorname" v-model="firstName" />
    <input type="text" placeholder="Nachname" v-model="lastName" />
    <input type="submit" value="AddUser" v-on:click="add" :disabled="!checkInputs" />
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "createuser",
  data() {
    return {
      firstName: "",
      lastName: "",
    };
  },
  methods: {
    add: async function () {
      if (this.firstName != "" && this.lastName != "") {
        await axios.post(
          `http://localhost:7071/api/user?firstname=${this.firstName}&lastname=${this.lastName}`
        );
        this.firstName = ""; 
        this.lastName = "";
      }
    },
  },
  computed:{
    checkInputs: function () {
      return this.firstName != "" && this.lastName != "";
    },
  },
};
</script>