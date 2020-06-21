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
                    <tr v-for="spells in searchSpells" :key="spells.id" v-on:click="edit(spells)">
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
        <div class="container is-fluid">


            <h1 class="title is-3 is-spaced">Edit the chosen Spell</h1>

            <div class="columns is-multiline is-mobile">
                <div class="column is-two-thirds"><input v-model="name" class="input is-primary" type="text" key="spellSlug" placeholder="Spell Name"></div>
                <div class="column is-2"><input v-model="kind_id" class="input is-primary" type="text"  placeholder="Kind Id"></div>

                <div class="column is-full"><input v-model="quote" class="input is-primary" type="text"  placeholder="Spell Quote"></div>

                <div class="column is-full"><textarea v-model="description" class="textarea is-primary" type="text" placeholder="Spell Description"></textarea></div>
            </div>

            <button class="button is-primary" type="submit" v-on:click="update(name, quote, description, kind_id, editSpells)">Submit</button>

        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {
                searchSpells: {},
                editSpells: {},
                q: "",
                name: "",
                quote:"",
                description:"",
                kind_id: ""
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
            },
            edit(spells) {
                this.name = spells.name
                this.quote = spells.quote
                this.description = spells.description
                this.kind_id = spells.kind_id
                this.editSpells = spells
                console.log('Edit spells called.')
            },
            update(name, quote, description, kind_id, editSpells) {
                axios
                    .put('/spell/'+ editSpells.slug, {name, quote, description, kind_id})
                    .then(({data}) => this.editSpells = data);
                console.log('Create spells called.')
            }
        }
    }
</script>
