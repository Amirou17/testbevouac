<template>
  <div class="container pt-5">
    <h2 class="bg-info text-muted sticky-top">Les 10 premières entreprises à fort potentiel d'embauche se trouvant à Paris ou Marseille</h2>
    <div class="row row-cols-1 row-cols-md-2 pt-5">
      <div class="container" :key="index" v-for="(entreprise, index) in entreprise">
        <div class="jumbotron col mb-7">
          <h3>{{ entreprise.name }}</h3>
          <hr>
          <h5>Nombre d'étoiles : <span class="badge badge-info">{{ entreprise.stars }}</span></h5>
          <h6>Adresse : {{ entreprise.address }}</h6>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'module1',
  data(){
    return{
      config : {
        headers: {
          'Authorization' : 'Bearer sh6E1PhnqmslbohYOwgXt3c3XMA'
        }
      },
      entreprise: null
    }
  },
  mounted() {
    axios
        .get('https://api.emploi-store.fr/partenaire/labonneboite/v1/company/?rome_codes_keyword_search=Informatique&page=1&page_size=10&departments=75,13', this.config)
        .then((reponse) => {
          this.entreprise = reponse.data.companies;
          //console.log(this.entreprise)
        }).catch((reason) => {console.log(reason)});
  }
}
</script>

<style scoped>
</style>