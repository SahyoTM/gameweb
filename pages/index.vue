<template>
  <div class="container">
    <Nav />
    <div v-for="recette in filteredRecettes" :key="recette.post_name">
      <NuxtLink :to="`recette/${recette.post_name}`">
        {{recette.post_title}}
      </NuxtLink>
    </div>

    <input type="text"  v-model="search"> 
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'homepage',
  data(){
    return {
      recettes: [],
      search:'',
    }
  },
  mounted(){
    axios.get("https://tmeyer.mmi.o2switch.site/gameweb/wp-json/wp/v2/type_recette").then(response => 
    this.recettes = response.data
    );
    console.log(this.recettes);
  },

  computed: {
    filteredRecettes() {
      //this.$nuxt.$on('searchEvent', () => {
        return this.recettes.filter(recette => {
          return recette.post_name.indexOf(this.search.toLowerCase()) > -1
          console.log(search)
        })
      }
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

.dark-mode p,.dark-mode th,.dark-mode td, .dark-mode svg{
  color:white !important;
}

.dark-mode body{
  background-color: #091A28;
  color:white;
}

.sepia-mode body{
  background-color: pink;
  color:black;
}
</style>