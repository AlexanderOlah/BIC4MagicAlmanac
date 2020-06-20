<template>
    <div>
        <div class="container is-fluid">
            <h1 class="title is-3 is-spaced">List of all Spells</h1>
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
                    <tr v-for="spells in listSpells" :key="spells.id">
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
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        },
        data() {
          return {
              listSpells: {}
          }
        },
        created() {
            axios.get('./list/spell')
            .then(({data}) => this.listSpells = data);
            console.log('List spells created.')
        }
    };
    methods: {

    }
</script>
