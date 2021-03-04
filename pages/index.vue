<template>
  <div class="container">
    <div>
      <li v-for="(recette, index) in recettes" :key="index"><NuxtLink :to="`recette/${recette.post_name}`">{{recette.post_title}}</NuxtLink></li>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'homepage',
  data(){
    return {
      recettes: [],
    }
  },
  mounted(){
    axios.get("https://tmeyer.mmi.o2switch.site/gameweb/wp-json/wp/v2/type_recette").then(response => this.recettes = response.data);
    console.log(this.recettes);
  }
}

</script>

<style>
.page-enter-active, .page-leave-active{
  transition: all 0.5s;
}

.page-enter, .page-leave-active{
  opacity: 0;
  transform: scale(0);
}


</style>