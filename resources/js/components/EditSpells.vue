<template>
    <div class="container is-fluid">
        <h1 class="title is-3 is-spaced">Search Spells by Keyword</h1>

        <div class="columns is-multiline is-mobile">
            <div class="column is-half"><input v-model="q" v-on:input="query(q)"  type="text" class="input is-primary" placeholder="Spell Name"></div>
        </div>
        <div class="table-container">
            <table class="table is-striped is-hoverable table-hover">
                <thead>
                <tr>
                    <th>ID</th>
                    <th>Slug</th>
                    <th>Name</th>
                    <th>Quote</th>
                    <th>Description</th>
                    <th>Kind</th>
                    <th>Created at</th>
                    <th>Updated at</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="spells in searchSpells" :key="spells.id">
                    <td>{{spells.id}}</td>
                    <td>{{spells.slug}}</td>
                    <td>{{spells.name}}</td>
                    <td>{{spells.quote}}</td>
                    <td>{{spells.description}}</td>
                    <td>{{spells.kind_id}}</td>
                    <td>{{spells.created_at}}</td>
                    <td>{{spells.updated_at}}</td>
                </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>


<script>
//SEARCH ZU EDIT -> data retun searchspell kopie von create

    export default {
        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {
                searchSpells: {}
            }
        },
        created() {

        },

        methods: {
            query(q) {
                axios
                    .post('/search/spell', {q})
                    .then(({data}) => this.searchSpells = data);
                console.log('Search spells called.')
            }
        }
    }
</script>
