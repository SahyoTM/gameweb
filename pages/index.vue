<template>
  <div class="container">
    <div>
      <input v-model="query" type="search" @change="fonction1" autocomplete="off" />

      <ul v-if="recettes.length">
        <li v-for="recette of recettes" :key="recette.post_name">
          <NuxtLink :to="`recette/${recette.post_name}`">{{ recette.post_title }}</NuxtLink>
        </li>
      </ul>
    </div> 

    <div>
      <h1>Color mode: {{ $colorMode.value }}</h1>
      <select v-model="$colorMode.preference">
        <option value="system">System</option>
        <option value="light">Light</option>
        <option value="dark">Dark</option>
        <option value="sepia">Sepia</option>
      </select>
    </div>

    <!-- <ColorModePicker /> -->
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'homepage',
  data(){
    return {
      recettes: [],
      query: '',
    }
  },
  mounted(){
    axios.get("https://tmeyer.mmi.o2switch.site/gameweb/wp-json/wp/v2/type_recette").then(response => this.recettes = response.data);
    console.log(this.recettes);
  },

  watch: {
    async query (query) {
      if (!query) {
        this.recettes = []
        return
      }

      /* this.recettes = await this.$content('recettes')
        .only(['post_title', 'post_name'])
        .limit(12)
        .search(query)
        .fetch() */
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