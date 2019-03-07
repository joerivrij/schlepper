 <template>
   <div>
   <version></version>
   <containers></containers>
   <images></images>
    <volumes></volumes>
   <networks></networks>
   </div>
 </template>


<script>
  //import your components here
  import Containers from './components/Containers.vue'
  import Images from './components/Images.vue'
  import Version from './components/Version.vue'
  import Networks from './components/Networks'
  import Volumes from './components/Volumes'
  export default {

    components: {
      'version': Version,
      'containers': Containers,
      'images' : Images,
      'networks' : Networks,
      'volumes': Volumes

    }

  }

 </script>
