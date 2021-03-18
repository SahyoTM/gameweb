<template>
  <div>
    <b-navbar toggleable="md" type="light" >

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item class="test"><NuxtLink to="/">ACCUEIL</NuxtLink></b-nav-item>
          <input type="text" @click="$nuxt.$emit(searchEvent, search)" v-model="search"> 
          <b-nav-item v-if="$colorMode.preference === 'dark'" @click="$colorMode.preference = 'light'"><b-icon icon="sun"></b-icon></b-nav-item>
           <b-nav-item v-if="$colorMode.preference === 'light'" @click="$colorMode.preference = 'dark'"><b-icon icon="moon"></b-icon></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  /* data(){
    return{
      search:'',  
    }   
  }, */
}

</script>

<style  >
nav a{
  color:#090409;
  font-weight: 700;
  margin-left:3rem;

  transition : all 0.5s;
}

.dark-mode nav a{
  color:white;
  font-weight: 700;
  margin-left:3rem;

  transition : all 0.5s;
}

nav li.test{
  margin-left: 10rem;
}

@media only screen and (max-width : 1224px) {
    nav li.test{
      margin-left: 0;
  }
}

nav a:hover{
  color:#090409;
  font-weight:700 !important;
  transition : all 0.5s;
  text-decoration:none !important;
}

.dark-mode nav a:hover{
  transition : all 0.5s;
}
</style>