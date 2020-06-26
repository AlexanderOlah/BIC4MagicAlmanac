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
                            <th>Description</th>
                            <th>Created at</th>
                            <th>Updated at</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr>
                            <td>{{createdKind.id}}</td>
                            <td>{{createdKind.slug}}</td>
                            <td>{{createdKind.name}}</td>
                            <td>{{createdKind.description}}</td>
                            <td>{{createdKind.created_at}}</td>
                            <td>{{createdKind.updated_at}}</td>
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
        name: "ModalKindsMessage",
        props: {
            messageTitle: {
                required: true,
                type: String
            },
            createdKind: {
                required: true,
            }
        },
        data() {
            return {
                modal_message: "",
                modal_showKinds: {},
            }
        },
        methods: {
            close() {
                this.$emit('close');
                console.log('ModalKindsMessage closed & cleared.')
            },
        }
    }
</script>

<style scoped>

</style>
