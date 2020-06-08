<template>
    <div>
        <h1>List Spells Component</h1>
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
