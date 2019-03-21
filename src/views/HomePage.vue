<template>
  <div>
    <!-- Nav -->
    <nav id="nav">
      <ul class="container">
        <li><a href="#top">Top</a></li>
        <li><a href="#containerDashboard">Containers</a></li>
        <li><a href="#imagesDashboard">Images</a></li>
        <li><a href="#volumesDashboard">Volumes</a></li>
        <li><a href="#networkDashboard">Networks</a></li>
      </ul>
    </nav>
    <version></version>
    <containers></containers>
    <images></images>
    <volumes></volumes>
    <networks></networks>
  </div>
</template>

<script>
  import Containers from '../components/Containers.vue'
  import Images from '../components/Images.vue'
  import Version from '../components/Version.vue'
  import Networks from '../components/Networks'
  import Volumes from '../components/Volumes'

  export default {
    name: 'homepage',
    data () {
      return {}
    },

    components: {
      'version': Version,
      'containers': Containers,
      'images' : Images,
      'networks' : Networks,
      'volumes': Volumes
    },
    computed: {
    },
  }
</script>
