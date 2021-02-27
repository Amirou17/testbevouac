<template>
  <div class="container w-75 pt-3">
    <div class="list row">
      <div class="col">
        <h4 class="pb-3">Listes des entreprises à fort potentiel d'embauche se trouvant à Paris ou Marseille</h4>
        <ul class="list-group" id="tutorials-list">
          <li
              class="list-group-item"
              :class="{ active: index === currentIndex }"
              v-for="(entreprise, index) in entreprises"
              :key="index"
          >
            <strong>{{ entreprise.name }}</strong> --- <span class="badge badge-info">{{ entreprise.stars }}</span> étoiles --- Adresse : {{ entreprise.address }}
          </li>
        </ul>
      </div>
      <div class="col-md-12 pt-2 ">
        <b-pagination
            v-model="page"
            :total-rows="count"
            :per-page="pageSize"
            prev-text="Prev"
            next-text="Next"
            @change="handlePageChange"
        ></b-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Moduel2',
  data(){
    return {
      config : {
        headers: {
          'Authorization' : 'Bearer pT1gt5QI36V7zYN9DRvms4zwcyk'
        }
      },
      entreprise: null,
      entreprises: [],
      currentIndex: -1,
      page: 1,
      count: 0,
      pageSize: 10,
    }
  },
  methods: {
    handlePageChange(value) {
      this.page = value;
      this.retrieveEntreprises();
    },
    retrieveEntreprises(){
      axios
          .get('https://api.emploi-store.fr/partenaire/labonneboite/v1/company/?rome_codes_keyword_search=Informatique&page='+this.page+'&page_size=10&departments=75,13', this.config)
          .then((reponse) => {
            this.entreprises = reponse.data.companies;
            this.count = reponse.data.companies_count;
          }).catch((reason) => {
        this.count = 200;
        console.log(reason)
      });
    }
  },
  mounted(){
    this.retrieveEntreprises();
  }
}
</script>

<style scoped>
</style>