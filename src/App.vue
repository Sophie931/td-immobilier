<template>
  <div id="app">
    <label>
      Afficher uniqument les biens vendus ?
      <input type="checkbox" v-model="afficherUniquementLesBiensVendus">
    </label>

    <BienAVendre
      v-for="(bien, index) in biensAAfficher"
      :key="bien.id"
      :titre="bien.titre"
      :type="bien.type"
      :prix="bien.prix"
      :contact="bien.contact"
      :vendu="bien.vendu"
      @modifier-etat-du-bien="(payload) => modifierEtatDuBien(index, payload)"
    ></BienAVendre>
    <!-- Lorsque l'enfant émet l'événement modifier-etat-du-bien, on appelle une méthode avec l'index du bien et son nouvel état -->
    <!-- Le composant BienAVendre n'est responsable que de l'affichage de la donnée, les appels API restent dans le parent -->


    <details>
      <summary>Ajout d'un bien</summary>
      <AjoutDeBien
        @ajouter-bien-a-vendre="ajouterBienAVendre"
      ></AjoutDeBien>
    </details>
  </div>
</template>

<script>
import axios from 'axios';
import BienAVendre from './components/BienAVendre'
import AjoutDeBien from './components/AjoutDeBien'

export default {
  name: 'app',
  data() {
    return {
      afficherUniquementLesBiensVendus: false,
      biens: [],
    };
  },
  computed: {
    biensAAfficher() {
      // On affiche tous les biens si aucun filtre n'est appliqué
      if (!this.afficherUniquementLesBiensVendus) {
        return this.biens
      }
      // Sinon, on n'affiche que ceux qui ne sont pas vendus
      return this.biens.filter(bien => !bien.vendu)
    },
  },
  components: {
    BienAVendre,
    AjoutDeBien,
  },
  methods: {
    modifierEtatDuBien(indexDuBien, nouvelEtat) {
      // On fait une copie du bien
      const copie = Object.assign({}, this.biens[indexDuBien])
      // On change l'état
      copie.vendu = nouvelEtat.vendu
      // Puis on met à jour via l'API
      axios.put(`http://localhost:3000/biens/${copie.id}`, copie)
        .then((reponse) => {
          // Lorsque l'API répond que la mise à jour est effectuée, on met à jour les données du composant
          this.biens[indexDuBien] = reponse.data
        })
    },
    ajouterBienAVendre(bienAVendre) {
      // On post un nouveau bien à vendre, en ajoutant l'attribut vendu à false
      const bienAEnregistrer = Object.assign({}, bienAVendre)
      bienAEnregistrer.vendu = false
      axios.post(`http://localhost:3000/biens/`, bienAEnregistrer)
        .then((reponse) => {
          // Lorsque l'API répond que l'ajout est effectué, on ajoute l'élément dans la liste
          this.biens.push(reponse.data)
        })
    },
  },
  created() {
    // Récupération des données depuis l'API
    axios.get('http://localhost:3000/biens')
      .then((reponse) => {
        this.biens = reponse.data
      })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
