<template>
  <div>
    <nav id="nav">
      <ul class="container">
        <router-link
          tag="a"
          :to="{name: 'homepage'}">
          Home
        </router-link>
      </ul>
    </nav>
    <h2>Container Details!!!!!!</h2>
    <dl>
      <dt>Container name</dt>
      <dd>{{(container.Names ? container.Names[0] : '')}}</dd>
      <dt>Container Id</dt>
      <dd>{{container.Id}}</dd>
    </dl>
    <button @click="startContainer()">
      <img src="../assets/images/icons/baseline-play_arrow-24px.svg" alt="playButton">
    </button>
    <button @click="stopContainer()">
      <img src="../assets/images/icons/baseline-stop-24px.svg" alt="stopButton">
    </button>
    <button @click="restartContainer()">
      <img src="../assets/images/icons/baseline-replay-24px.svg" alt="replayButton">
    </button>
  </div>
</template>

<script>
  export default {
    name: 'containerdetail',
    data () {
      return {
        container: {},
        containerId: this.$route.params.containerId,
         }
    },

    computed: {
    },

    methods: {
      getAllContainers: function () {
          this.$apiClient.get(`http://0.0.0.0:3000/dockers/containers/${this.containerId}`)
            .then((response) => {
              this.container = response.data;
            })
            .catch(e => {
              this.errors.push(e)
            })
      },
      startContainer: () => {
        console.log("hello Johan")
      },
      stopContainer: () => {
        console.log("bye Johan")
      },
      restartContainer: () => {
        console.log("again Johan")
      },

    },

    mounted() {
      this.getAllContainers();
    }
  }
</script>

<style>
</style>
