<template>
    <div>
        <div class="container is-fluid">


            <h1 class="title is-3 is-spaced">Create a new Spell</h1>

            <div class="columns is-multiline is-mobile">
                <div class="column is-two-thirds"><input v-model="name" class="input is-primary" type="text"  placeholder="Spell Name"></div>

                <div class="column is-one-third">
                    <div class="field is-horizontal">
                        <label class="field-label is-normal">Kind Id:</label>
                        <div class="control">
                            <div class="select is-primary">
                                <select v-model="kind_id" class="form-control select">
                                    <option v-for="kinds in listKinds" :key="kinds.id">{{kinds.id}}</option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="column is-full"><input v-model="quote" class="input is-primary" type="text"  placeholder="Spell Quote"></div>

                <div class="column is-full"><textarea v-model="description" class="textarea is-primary" type="text" placeholder="Spell Description"></textarea></div>
            </div>

            <button class="button is-primary" type="submit" v-on:click="create(name, quote, description, kind_id)">Submit</button>

        </div>

    </div>
</template>

<script>
    export default {
        name: "CreateSpells",

        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {
                name:"", quote:"", description:"", kind_id:"",
                createSpells: {},
                listKinds: {}
            }
        },
        created() {
            axios.get('/list/kind')
                .then(({data}) => this.listKinds = data);
            console.log('List kinds created.')
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
