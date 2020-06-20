<template>
    <div>
        <div class="container is-fluid">
            <h1 class="title is-3 is-spaced">List of all Kinds</h1>
            <div class="table-container">
                <table class="table is-striped is-hoverable table-hover">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Slug</th>
                            <th>Name</th>
                            <th>Description</th>
                            <th>Created at</th>
                            <th>Updated at</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="kinds in listKinds" :key="kinds.id">
                            <td>{{kinds.id}}</td>
                            <td>{{kinds.slug}}</td>
                            <td>{{kinds.name}}</td>
                            <td>{{kinds.description}}</td>
                            <td>{{kinds.created_at}}</td>
                            <td>{{kinds.updated_at}}</td>
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
              listKinds: {}
          }
        },
        created() {
            axios.get('./list/kind')
            .then(({data}) => this.listKinds = data);
            console.log('List kinds created.')
        }
    };
    methods: {

    }
</script>
