<template>
  <div class="container pt-5">
    <h2 class="bg-info text-muted sticky-top">Les 10 premières entreprises à fort potentiel d'embauche se trouvant à Paris ou Marseille</h2>
    <div class="row row-cols-1 pt-5">
      <div class="container" :key="index" v-for="(entreprises, index) in entreprises">
        <div class="jumbotron col mb-7">
          <h3>{{ entreprises.name }}</h3>
          <hr>
          <h5>Nombre d'étoiles : <span class="badge badge-info">{{ entreprises.stars }}</span></h5>
          <h6>Adresse : {{ entreprises.address }}</h6>
          <div v-if="10" v-observe-visibility="handleScrolled" ></div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import axios from 'axios'
  import VueObserveVisibility from 'vue-observe-visibility'
  import Vue from 'vue'
  Vue.use(VueObserveVisibility)
  export default {
    name: 'Module3',
    data(){
      return {
        config : {
          headers: {
            'Authorization' : 'Bearer bRiG_XgMM0rn0nUZOb7bRPnBad0' /*Le token*/
          }
        },
        entreprises: [],
        estVisible: false,
        page: 1,
        nbEntreprises : 0,
        dernierePage: 0,
      }
    },
    methods: {
      async fetch(){
        let entreprises = await axios.get('https://api.emploi-store.fr/partenaire/labonneboite/v1/company/?rome_codes_keyword_search=Informatique&page_size=10&departments=75,13&page='+this.page, this.config)

        this.entreprises.push(...entreprises.data.companies)

        this.dernierePage = Math.ceil(entreprises.data.companies_count/10)
        //console.log(this.dernierePage)
      },
      handleScrolled (estVisible){
        if (!estVisible){
          return
        }
        //S'arrete quand la page courante >= à la derniere page
        if(this.page >= this.dernierePage){
          return
        }
        this.page++
        this.fetch()
      },
    },
    mounted() {
      this.fetch()
    }
  }
</script>