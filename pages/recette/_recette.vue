<template>
    <b-container id="recette">
        <Nuxtlink class="back_link" @click="$router.back()"><b-icon icon="chevron-double-left" variant="dark"></b-icon> Retour en arrière </Nuxtlink>
        <p>Visites totales sur le site: {{this.$store.state.analytics.pageVisits}}</p>
        <h1 class="text-center font-weight-bold h1 text-uppercase">{{recette.post_title}}</h1>

        <div class="text-center">
            <b-img rounded :src="url" :alt="recette.post_name"></b-img>
        </div>

        <div class="table-responsive">
            <table class="table text-center">
            <thead>
                <tr>
                <th class="text-center" scope="col">DURÉE</th>
                <th class="text-center" scope="col">PERSONNE(S)</th>
                <th class="text-center" scope="col">DIFFICULTÉE</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                <td class="text-center">{{duree}}</td>
                <td class="text-center">{{personnes}}</td>
                <td class="text-center">{{difficultee}}</td>
                </tr>
            </tbody>
            </table>
        </div>
        
        <div class="row">
            <div class="col-md-6">
                <li v-for="(ingredient, i) in ingredients" :key="i">{{ingredients[i].nom_ingredient}} - {{ingredients[i].grammage_ingredient}}</li>
            </div>

            <div class="col-md-6">
                <li v-for="(etape, j) in etapes" :key="j">{{etapes[j].numero_etape}} - {{etapes[j].description_etape}}</li>
            </div>
        </div>
        
        
    </b-container>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            recette:[],
            ingredients:[],
            etapes:[],
        }
    },
    mounted(){
        let nbr = this.$route.params.recette;
        axios.get("https://tmeyer.mmi.o2switch.site/gameweb/wp-json/wp/v2/type_recette").then(response => { 
            // this.recette = response.data[nbr];
            let ifn = response.data.filter(x => x.post_name == nbr);
            this.recette = ifn[0];
            this.duree = ifn[0].acf.duree;
            this.personnes = ifn[0].acf.personnes;
            this.difficultee = ifn[0].acf.difficultee[0];
            this.url = ifn[0].acf.image_recette.sizes.medium;
            this.ingredients = ifn[0].acf.liste_ingredients;
            this.etapes = ifn[0].acf.etapes_recette;
            console.log(this.ingredients);
            });
        
    },
    middleware ({ store }) {
        store.commit('analytics/increment')
    }    
}   
</script>

<style>
#recette li{
    list-style: none;
}

h1,h2{
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
}

img{
    height:25%;
    margin:1rem;
}

.back_link{
    font-weight:700;
}

.back_link:hover{
    font-weight:700;
    text-decoration: underline;
    cursor:pointer;
}
</style>