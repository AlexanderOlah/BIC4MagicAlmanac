<template>
    <div>
        <h1>List Kinds Component</h1>
        <table class="table table-hover">
            <tbody>
            <tr>
                <th>id</th>
                <th>slug</th>
                <th>name</th>
                <th>description</th>
                <th>created_at</th>
                <th>updated_at</th>
            </tr>
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
