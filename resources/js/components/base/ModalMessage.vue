<template>
    <div class="modal" v-model="createdSpell.description" v-on:mouseenter="query(createdSpell.description)">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
                <p class="modal-card-title" >{{messageTitle}}</p>
                <button class="delete" @click="close" aria-label="Close modal"></button>
            </header>
            <section class="modal-card-body">

                <h1>You just created:</h1>

                <div class="table-container" style="padding-top: 25px">
                    <table class="table">
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
                        <tr v-for="spells in modal_showSpells">
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

            </section>
            <footer class="modal-card-foot">
                <button class="button is-primary" @click="close" aria-label="Close modal">OK</button>
            </footer>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ModalMessage",
        props: {
            messageTitle: {
                required: true,
                type: String
            },
            createdSpell: {
                required: true,
            }
        },
        data() {
            return {
                modal_message: "",
                modal_showSpells: {},
            }
        },
        methods: {
            close() {
                this.$emit('close');
                console.log('ModalMessage closed & cleared.')
            },
            query(q){
                console.log('Testing: Description for this call before searchSpell was ' + q)
                axios
                    .post('/search/spell', {q})
                    .then(({data}) => this.modal_showSpells = data);
                console.log('searchSpell called.')
            }
        }
    }
</script>

<style scoped>

</style>
