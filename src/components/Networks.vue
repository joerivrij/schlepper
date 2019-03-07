<template>
  <!-- networks -->
  <article id="networks" class="wrapper style3">
    <div class="container">
      <header>
        <h2>Network Dashboard</h2>
      </header>
    </div>
    <div class="network">
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
    </div>
  </article>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "Networks.vue",
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
  span.image{
    width: 20%;
    height: 20%;
  }
  table{
    width:100%;
    table-layout: fixed;
  }
  .tbl-header{
    background-color: rgb(255,250,250);
    margin-top: 50px;
    margin-bottom: 0px;
  }
  .tbl-content{
    height:400px;
    overflow-x:auto;
    margin-top: 0px;
    background-color: rgb(255,255,255);
    border: 1px solid #999999;
  }
  th{
    padding: 20px 15px;
    text-align: left;
    font-weight: bold;
    font-size: 24px;
    color: #4682B4;
    text-transform: uppercase;
  }
  td{
    padding: 15px;
    text-align: left;
    vertical-align:middle;
    font-weight: 300;
    font-size: 16px;
    color: #4682B4;
    border-bottom: solid 1px #999999;
  }

</style>
