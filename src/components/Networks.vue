<template>
  <!-- networks -->
  <div class="container" id="networkDashboard">
      <header>
        <h2>Network Dashboard</h2>
      </header>
      <button id="getNetworks" class="" v-on:click="getNetworks">Get Networks</button>
      <div v-if="networks">
      </div>
      <div class="tbl-header">
        <table cellpadding="0" cellspacing="0" border="0">
          <thead>
          <tr>
            <th>Name</th>
            <th>Id</th>
            <th>Scope</th>
            <th>Driver</th>
          </tr>
          </thead>
        </table>
      </div>
      <div class="tbl-content">
        <table cellpadding="0" cellspacing="0" border="0">
          <tbody>
          <tr v-for="network of networks">
            <td>{{network.Name}}</td>
            <td>{{network.Id.substring(0, 11)}}</td>
            <td>{{network.Scope}}</td>
            <td>{{network.Driver}}</td>
          </tr>
          </tbody>
        </table>
      </div>
      </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "Networks",
    data() {
      return {
        networks: []
      }
    },
    created() {
    },
    methods: {
      getNetworks: function () {
        axios.get("http://0.0.0.0:3000/dockers/networks")
          .then((response) => {
            this.networks = response.data;
          })
          .catch(e => {
            console.log(e)
          })
      }
    }
  }

</script>

<style scoped>

</style>
