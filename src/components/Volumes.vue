<template>
  <!-- volumes -->
    <div class="container" id="volumesDashboard">
      <header>
        <h2>Volumes Dashboard</h2>
      </header>
      <button id="getNetworks" class="" v-on:click="getVolumes">Get Volumes</button>
      <div v-if="volumes">
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
    name: "Volumes",
    data() {
      return {
        volumes: []
      }
    },
    created() {
    },
    methods: {
      getVolumes: function () {
        axios.get("http://0.0.0.0:3000/dockers/volumes")
          .then((response) => {
            this.volumes = response.data;
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
