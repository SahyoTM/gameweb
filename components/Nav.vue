<template>
  <div>
    <b-navbar toggleable="md" type="light" variant="secondary">

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item class="test"><NuxtLink to="/">ACCUEIL</NuxtLink></b-nav-item>
          <b-nav-item ><NuxtLink to="/digitalArt">DIGITAL ART</NuxtLink></b-nav-item>
          <b-nav-item ><NuxtLink to="/projet">PROJET</NuxtLink></b-nav-item>
          <b-nav-item ><NuxtLink to="/blog">BLOG</NuxtLink></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
}
</script>

<style  >
nav a{
  color:#090409;
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

nav a:hover,nav a:focus{
  color:#090409;
  font-weight: 900;
  text-decoration: none;
}

nav a:hover{
  transition : all 0.5s;
}

nav.bg-secondary{
  background-color: rgba(255, 255, 255, 0.2) !important;
}
</style>