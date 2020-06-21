<template>
    <div>
        <div class="container is-fluid">
            <div>
                <h1 class="title is-3 is-spaced" >Edit the chosen Kind</h1>

                <div class="columns is-multiline is-mobile">
                    <div class="column is-two-thirds"><input v-model="name" class="input is-primary" type="text" key="kindSlug" placeholder="Kind Name"></div>
                    <div class="column is-full"><textarea v-model="description" class="textarea is-primary" type="text" placeholder="Kind Description"></textarea></div>
                </div>

                <button class="button is-primary" type="submit" v-on:click="update(name, description, editKinds)">Submit</button>
            </div>

            <h1 class="title is-3 is-spaced" style="padding-top: 100px">List of all Kinds</h1>
            <div class="table-container" >
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
                        <tr v-for="kinds in listKinds" :key="kinds.id" v-on:click="edit(kinds)">
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
              name: "",
              description: "",
              editKinds: {},
              listKinds: {}
          }
        },
        created() {
            axios.get('./list/kind')
            .then(({data}) => this.listKinds = data);
            console.log('List kinds created.')
        },

        methods: {
            edit(kinds) {
                this.name = kinds.name
                this.description = kinds.description
                this.editKinds = kinds
                console.log('Edit kinds called.')
            },
            update(name, description, editKinds) {
                axios
                    .put('/kind/'+ editKinds.slug, {name, description})
                    .then(({data}) => this.editKinds = data);
                console.log('Update kinds called.')
            }
        }
    };
</script>
