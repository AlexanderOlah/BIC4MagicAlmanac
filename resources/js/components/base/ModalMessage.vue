<template>
    <div class="modal">
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
                        <tr>
                            <td>{{createdSpell.id}}</td>
                            <td>{{createdSpell.slug}}</td>
                            <td>{{createdSpell.name}}</td>
                            <td>{{createdSpell.quote}}</td>
                            <td>{{createdSpell.description}}</td>
                            <td>{{createdSpell.kind_id}}</td>
                            <td>{{createdSpell.created_at}}</td>
                            <td>{{createdSpell.updated_at}}</td>
                        </tr>
                        </tbody>
                    </table>
                </div>

            </section>
            <footer class="modal-card-foot">
                <button class="button is-primary" @click="close" aria-label="Close modal">OK</button>
                <button class="button is-primary" @click="getNew(createdSpell)" aria-label="Close modal">Get</button>
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
                modal_showSpells:""
            }
        },
        methods: {
            close() {
                this.$emit('close');
                console.log('ModalMessage closed & cleared.')
            },
            getNew(createdSpell){
                axios
                    .get('/spell/'+ createdSpell.slug)
                    .then(({data}) => this.modal_showSpells = data);
                console.log('getNew spells called.')
                console.log('Testing: Slug for this call was .' + createdSpell.slug)
            }
        }
    }
</script>

<style scoped>

</style>
