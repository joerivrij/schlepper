<template>
  <!-- Containers -->
  <article id="container" class="wrapper style2">
    <div class="container">
      <header>
        <p>A listing of the current known containers</p>
      </header>
  <div class="containers">
    <button id="getContainers" style="background-color:#2196F3;" v-on:click="getAllContainers">Get Containers</button>
    <h2 v-if="checked == true">Running</h2>
    <h2 v-else>All</h2>
    <label class="switch">
      <input v-model="checked" type="checkbox" id="checkbox" >
      <span class="slider round"></span>
    </label>
      <div class="tbl-header">
        <table cellpadding="0" cellspacing="0" border="0">
          <thead>
      <tr>
        <th>Image</th>
        <th>Id</th>
        <th>State</th>
        <th>Port</th>
      </tr>
          </thead>
        </table>
    <div class="tbl-content">
      <table cellpadding="0" cellspacing="0" border="0">
        <tbody>
      <tr v-for="container of containers">
        <td>{{container.Image.split(':')[0]}}</td>
        <td>{{container.Id.substring(0, 11)}}</td>
        <td>{{container.State}}</td>
        <td v-if="container.Ports == false">
          none
        </td>
        <td v-if="container.Ports[0]">
          {{container.Ports[0].PrivatePort}}
        </td>
      </tr>
        </tbody>
    </table>
    </div>
      </div>
    <h2>Container templates</h2>
    <div class="row aln-center">
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/gopher.png"/>
          <h3>Golang</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/nodejs.png"/>
          <h3>Nodejs</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/python.png"/>
          <h3>Python</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/java.jpg"/>
          <h3>Java</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/nginx.jpg"/>
          <h3>Nginx</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="static/images/dotcore.png"/>
          <h3>Dotnet core</h3>
        </section>
      </div>
    </div>
  </div>
    </div>
  </article>
</template>

<script>
    import axios from 'axios';
    export default {
      name: "Containers.vue",
      data() {
          return {
            containers: [],
            errors: [],
            checked: ''
          }
        },
        created() {
          setInterval(function () {
            this.getAllContainers();
          }.bind(this), 10000);
        },

        methods: {
          getAllContainers: function () {
            if (!this.checked) {
            axios.get("http://0.0.0.0:3000/dockers/containers")
              .then((response) => {
                this.containers = response.data;
              })
              .catch(e => {
                this.errors.push(e)
              })}
              else {
              axios.get("http://0.0.0.0:3000/dockers/containers/running")
                .then((response) => {
                  this.containers = response.data;
                })
                .catch(e => {
                  this.errors.push(e)
                })
            }
          },

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
    height:300px;
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
  /* The switch - the box around the slider */
  .switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }

  /* Hide default HTML checkbox */
  .switch input {display:none;}

  /* The slider */
  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: .4s;
    transition: .4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
  }

  input:checked + .slider {
    background-color: #2196F3;
  }

  input:focus + .slider {
    box-shadow: 0 0 1px #2196F3;
  }

  input:checked + .slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
  }

  .slider.round:before {
    border-radius: 50%;
  }

	.image {
    height: 10%;
    width: 10%;
	}

</style>
