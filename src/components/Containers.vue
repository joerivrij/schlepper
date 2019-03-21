<template>
  <!-- Containers -->
  <div class="container" id="containerDashboard">
    <header>
      <h2>Container Dashboard</h2>
    </header>
    <button id="getContainers" class="" v-on:click="getAllContainers">Get Containers</button>
    <h2 v-if="checked == true">Running</h2>
    <h2 v-else>All</h2>
    <label class="switch">
      <input v-model="checked" type="checkbox" id="checkbox" >
      <span class="slider round"></span>
    </label>
      <div class="tbl-header tbl-header-container">
        <table cellpadding="0" cellspacing="0" border="0">
          <thead>
      <tr>
        <th>Image</th>
        <th>Id</th>
        <th>State</th>
        <th>Port</th>
        <th>Actions</th>
      </tr>
          </thead>
        </table>
    <div class="tbl-content tbl-content-container">
      <table cellpadding="0" cellspacing="0" border="0">
        <tbody>
        <tr v-for="container of containers"
        :class="{container_running: container.State === 'running',
                 container_stopped: container.State !== 'running'}">
          <td>{{container.Image.split(':')[0]}}</td>
          <td>
            <router-link
              tag="a"
              :to="{name: 'containerDetail', params: { containerId: container.Id}}">
              {{container.Id.substring(0, 11)}}
            </router-link>
          </td>
          <td>{{container.State}}</td>
          <td v-if="container.Ports == false">
            none
          </td>
          <td v-if="container.Ports[0]">
            {{container.Ports[0].PrivatePort}}
          </td>
          <td class="action-hovers">
            <i v-if="container.State !== 'exited'" @click='stopContainer(container.Id)' style="margin-right: 1rem;" class="fa fa-stop fa-lg"></i> <i style="margin-right: 1rem;" class="fa fa-random fa-lg" @click='restartContainer(container.Id)'></i> <i v-if="container.State !== 'running'" class="fa fa-play fa-lg" @click='startContainer(container.Id)'></i>
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
          <img class="image" src="../assets/images/gopher.png"/>
          <h3>Golang</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="../assets/images/nodejs.png"/>
          <h3>Nodejs</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="../assets/images/python.png"/>
          <h3>Python</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="../assets/images/java.jpg"/>
          <h3>Java</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="../assets/images/nginx.jpg"/>
          <h3>Nginx</h3>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <img class="image" src="../assets/images/dotcore.png"/>
          <h3>Dotnet core</h3>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios';
    export default {
      name: "Containers",
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
          startContainer: (id) => {
            console.log(`hello Johan ${id}`)
          },
          stopContainer: (id) => {
            console.log(`bye Johan ${id}`)
          },
          restartContainer: (id) => {
            console.log(`again Johan ${id}`)
          },
        }
    }
</script>

<style scoped>

  span.image{
    width: 20%;
    height: 20%;
  }

  /* The switch - the box around the slider */
  .switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }

  .container_running {
    background-color: #3CB371;
  }

  .container_running td, .container_running a  {
    color: white;
  }

  .container_stopped {
    background-color: #D3D3D3;
  }

  .container_stopped td, .container_stopped a  {
    color: #778899;
  }

  .action-hovers:hover i {
    cursor: pointer;
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
