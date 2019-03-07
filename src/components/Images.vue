
<template>
  <!-- Images -->
  <article id="images" class="wrapper style3">
    <div class="container">
      <header>
        <h2>Image Dashboard</h2>
      </header>
    </div>
    <div class="images">
      <button id="getImages" class="" v-on:click="getAllImages">Get Images</button>
      <div v-if="images">
        <div class="tbl-header">
          <table cellpadding="0" cellspacing="0" border="0">
            <thead>
            <tr>
              <th>Image</th>
              <th>Tag</th>
              <th>Id</th>
              <th>Size</th>
            </tr>
            </thead>
          </table>
        </div>
        <div class="tbl-content">
          <table cellpadding="0" cellspacing="0" border="0">
            <tbody>
            <tr v-for="image of images" v-if="image.RepoTags != null">
              <td> {{image.RepoTags[0].split(':')[0]}} </td>
              <td> {{image.RepoTags[0].split(':')[1]}} </td>
              <td> {{image.ID.split(':')[1].substring(0, 11)}} </td>
              <td> {{Math.ceil(image.Size / 1000000) + 'mb'}} </td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <h2>Image templates</h2>
    <div class="row aln-center">
      <div class="col-4 col-6-medium col-12-small">
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
  </article>
</template>


<script>
  import axios from 'axios';
  export default {
    name: "Images.vue",
    data() {
      return {
        images: []
      }
    },
    created() {
    },
    methods: {
      getAllImages: function () {
        axios.get("http://0.0.0.0:3000/dockers/images")
          .then((response) => {
            this.images = response.data;
            console.log(this.images[0])
          })
          .catch(e => {
            console.log(e)
          })
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
    height:600px;
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

  	.image {
      height: 10%;
      width: 10%;
  	}
</style>
