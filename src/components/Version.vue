<template>
  <!-- Home -->
  <div id="top" class="toppage">
      <img class="image" src="../assets/images/lotse_gopher.png"/>
      <header>
        <h1>Moin Moin beim Lotse!</h1>
      </header>
      <h2>{{version}}</h2>
      <a href="#containerDashboard" class="button large scrolly">Let's see the harbour area</a>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
      name: "Version",
      data() {
        return {
          version: 'No version',
        }
      },
      created() {
        this.getVersion();
      },
      methods: {
        getVersion: function () {
          axios.get("http://0.0.0.0:3000/dockers/version")
            .then((response) => {
              this.version = response.data['dockerVersion']
            })
            .catch(e => {
              console.log(e)
            })
        },
      }
    }

</script>

<style scoped>

  .toppage {
    box-shadow: inset 0px 1px 0px 0px rgba(0, 0, 0, 0.05), inset 0px 2px 3px 0px rgba(0, 0, 0, 0.1);
    padding: 8em 0 8em 0;
    text-align: center;
    position: relative;
  }

  .toppage::after {
    background-image: url("../assets/images/hamburg_hafen_grey.jpg");
    opacity: 0.5;
    position: absolute;
    content: "";
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }

	.image {
		display: inline-block;
		position: relative;
    height: 25%;
    width: 25%;
	}
</style>

