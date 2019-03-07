<template>
  <!-- Home -->
  <article id="top" class="wrapper style1">
    <div class="container">
      <div class="row">
        <div class="col-4 col-5-large col-12-medium">
          <img class="image" src="static/images/lotse_gopher.png"/>
        </div>
        <div class="col-8 col-7-large col-12-medium">
          <header>
            <h1>Moin Moin beim Lotse!</h1>
          </header>
          <h2>{{version}}</h2>
          <p>And this is <strong>Lotse</strong></p>
          <a href="#container" class="button large scrolly">Let's see the harbour area</a>
        </div>
      </div>
    </div>
  </article>
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
	.image {
		display: inline-block;
		position: relative;
    height: 50%;
    width: 50%;
	}
</style>

