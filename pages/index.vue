<template>
  <div class="container">
    <div>
      <ul><li v-for="(recette, index) in recettes" :key="index"><NuxtLink :to="`recette/${recette.post_name}`">{{recette.post_title}}</NuxtLink></li></ul>
    </div>

    <div>
    <input v-model="query" type="search" autocomplete="off" />

    <ul v-if="recettes.length">
      <li v-for="recette of recettes" :key="recette.slug">
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">{{ article.title }}</NuxtLink>
      </li>
    </ul>
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

      this.articles = await this.$content('recettes')
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .limit(12)
        .search(query)
        .fetch()
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