<template>
    <!-- On annule le comportement par défaut pour ne pas naviguer -->
    <form @submit.prevent>
        <label>
            Titre
            <input type="text" v-model="nouveauBien.titre">
        </label>
        <label>
            Type
            <select v-model="nouveauBien.type">
                <option value="" disabled>Choisissez un type de bien à vendre</option>
                <option value="maison">Maison</option>
                <option value="appartement">Appartement</option>
            </select>
        </label>
        <label>
            Prix
            <input type="number" v-model.number="nouveauBien.prix">
        </label>
        <label>
            Contact
            <input type="text" v-model="nouveauBien.contact">
        </label>
        <button :disabled="!bienValide" @click="ajouter">Ajouter</button>
    </form>
</template>

<script>
// TODO: Validation
export default {
    name: 'AjoutDeBien',
    data() {
        return {
            nouveauBien: {
                titre: '',
                type: '',
                prix: 0,
                contact: ''
            }
        }
    },
    computed: {
        bienValide() {
            return this.nouveauBien.titre && this.nouveauBien.type && this.nouveauBien.contact && this.nouveauBien.prix > 0
        }
    },
    methods: {
        ajouter() {
            // Encore une fois, ce composant n'a que la responsabilité d'afficher le formulaire
            // L'appel API est laissé au parent
            this.$emit('ajouter-bien-a-vendre', {
                // On récupère toutes les données du nouveauBien (syntaxe équivalente à rajouter les champs un par un)
                ...this.nouveauBien
            })
        }
    },
}
</script>

<style>

</style>