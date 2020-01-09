<template>
  <section class="bien">
      <ul>
          <li>{{titre}}</li>
          <li>Type: {{type}}</li>
          <li>Prix: {{prix}}</li>
          <li>Contact: {{contact}}</li>
          <input type="checkbox" :checked="vendu" @change="modifierEtatDeVendu">
      </ul>
  </section>
</template>

<script>
export default {
    name: 'BienAVendre',
    props: {
        titre: {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: true
        },
        prix: {
            // Le prix peut être une chaine de caractère ou un nombre
            type: String|Number,
            required: true
        },
        contact: {
            type: String,
            // Valeur par défaut
            default: 'Pas de contact'
        },
        vendu: {
            type: Boolean,
            required: true
        },
    },
    methods: {
        modifierEtatDeVendu() {
            // Le composant enfant n'a pas la responsabilité de modifier la props
            // Il se contente de notifier son parent (App.vue) qu'une action est attendue de sa part
            this.$emit('modifier-etat-du-bien', {
                vendu: !this.vendu
            })
        }
    }
}
</script>

<style>

</style>