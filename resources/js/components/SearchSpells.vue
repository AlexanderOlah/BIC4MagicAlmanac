<template>
    <div>
        <h1>Search Spells by ID</h1>

        <input v-on:input="query()"  type="number" name="q" min="1" placeholder="1">
        <table class="table table-hover">
            <tbody>
            <tr>
                <th>id</th>
                <th>slug</th>
                <th>name</th>
                <th>quote</th>
                <th>description</th>
                <th>kind_id</th>
                <th>created_at</th>
                <th>updated_at</th>
            </tr>
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
</template>

<script>
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
            query() {
                axios
                    .post('/search/spell', {q: "q"})
                    .then(({data}) => this.searchSpells = data);
                console.log('Search spells called.')
            }
        }
    }
</script>
