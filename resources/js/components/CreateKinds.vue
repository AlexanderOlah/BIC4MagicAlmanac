<template>
    <div>
        <div class="container is-fluid">


            <h1 class="title is-3 is-spaced" >Create a new Kind</h1>

            <div class="columns is-multiline is-mobile">
                <div class="column is-two-thirds"><input v-model="name" class="input is-primary" type="text"  placeholder="Kind Name"></div>

                <div class="column is-full"><textarea v-model="description" class="textarea is-primary" type="text" placeholder="Kind Description"></textarea></div>
            </div>

            <button class="button is-primary" type="submit" v-on:click="create(name, description)">Submit</button>

        </div>

    </div>
</template>

<script>
    export default {
        name: "CreateKinds",

        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {
                name:"", description:"",
                createKinds: {}
            }
        },
        created() {

        },

        methods: {
            create(name, description) {
                axios
                    .post('/kind', {name, description})
                    .then(({data}) => this.createKinds = data);
                console.log('Create kinds called.')
            }
        }
    }

</script>

