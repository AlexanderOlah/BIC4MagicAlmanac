<template>
    <div>
        <div class="container is-fluid">


            <h1 class="title is-3 is-spaced">Edit the chosen Spell</h1>

            <div class="columns is-multiline is-mobile">
                <div class="column is-two-thirds"><input v-model="name" class="input is-primary" type="text" :key="spellSlug" :placeholder="spellSlug"></div>
                <div class="column is-2"><input v-model="kind_id" class="input is-primary" type="text"  placeholder="Kind ID"></div>

                <div class="column is-full"><input v-model="quote" class="input is-primary" type="text"  placeholder="Spell Quote"></div>

                <div class="column is-full"><textarea v-model="description" class="textarea is-primary" type="text" placeholder="Spell Description"></textarea></div>
            </div>

            <button class="button is-primary" type="submit" v-on:click="create(name, quote, description, kind_id)">Submit</button>

        </div>

    </div>
</template>

<script>
    export default {
        name: "EditSpells",
        props: {
            spellSlug: {
                required: true
            }
        },

        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {


            }
        },
        created() {
            axios
                .get('/edit/'+ this.spellSlug +'/spell')
                .then(({data}) => this.editSpells = data);
            console.log('Edit spells created.')
        },

        methods: {
            create(name, quote, description, kind_id) {
                axios
                    .post('/spell', {name, quote, description, kind_id})
                    .then(({data}) => this.createSpells = data);
                console.log('Create spells called.')
            }
        }
    }
</script>

<style scoped>

</style>
