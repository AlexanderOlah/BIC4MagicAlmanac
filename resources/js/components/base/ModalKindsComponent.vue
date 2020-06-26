<template>
    <transition name="modal-fade">
        <div class="modal" v-on:mouseenter="fill()">
            <div class="modal-background"></div>
            <div class="modal-card">
                <header class="modal-card-head">
                    <p class="modal-card-title">Edit Entry</p>
                    <button class="delete" @click="close" aria-label="close"></button>
                </header>
                <section class="modal-card-body">
                    <!-- Content ... -->
                    <div class="columns is-multiline is-mobile">
                        <div class="column is-two-thirds"><input v-model="modal_name" class="input is-primary" type="text"  placeholder="Kind Name"></div>
                        <div class="column is-full"><textarea v-model="modal_description" class="textarea is-primary" type="text" placeholder="Kind Description"></textarea></div>
                    </div>

                </section>
                <footer class="modal-card-foot">
                    <button class="button is-primary" type="submit" v-on:click="update(modal_name, modal_description, modal_editKinds)">Save changes</button>
                    <button type="button" class="button is-primary" @click="fill" aria-label="Fill modal">Show previous/Reset</button>
                    <button type="button" class="button is-primary" @click="close" aria-label="Close modal">Cancel</button>
                </footer>
            </div>

            <ModalKindsMessage
                v-show="isModalKindsMessageVisible"
                @close="closeModalKindsMessage"
                :messageTitle=this.messageTitle
                :created-kind=this.createdKind
            />

        </div>
    </transition>

</template>
<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        display: flex;
        flex-direction: column;
    }


</style>
<script>
    import ModalKindsMessage from "./ModalKindsMessage";
    export default {
        name: 'ModalKindsComponent',
        components: {
            ModalKindsMessage,
        },
        props: {
            name: {
                required: true,
                type: String
            },
            description: {
                required: true,
                type: String
            },
            slug:{
                required: true,
                type: String
            },
            editKinds:{
                required: true
            }


        },

        data() {
            return {
                modal_editKinds: {},
                modal_name: "",
                modal_description:"",
                modal_slug:"",
                modal_showKinds: {},
                isModalKindsMessageVisible: false,
                messageTitle:"",
                createdKind: {}
            }
        },
        methods: {
            close() {
                this.modal_name = ""
                this.modal_description = ""
                this.modal_slug = ""
                this.modal_editKinds = ""
                this.$emit('close');
                console.log('Modal closed & cleared.')
            },
            fill(){
                this.modal_name = this.name
                this.modal_description = this.description
                this.modal_slug = this.slug
                this.modal_editKinds = this.editKinds
                console.log('Modal filled.')
            },
            update(name, description, editKinds) {
                axios
                    .put('/kind/'+ editKinds.slug, {name, description})
                    .then(({data}) => this.modal_editKinds = data);
                console.log('Update kinds called.')
                this.showModalKindsMessage("Success!", editKinds);
            },
            // for our success/fail message popup
            showModalKindsMessage(messageTitle, editKinds) {

                this.messageTitle = messageTitle
                this.createdKind = editKinds
                this.isModalKindsMessageVisible = true

                console.log('showModal called.')
                console.log('Testing: Slug of the entry we changed is ' + editKinds.slug)
            },
            closeModalKindsMessage() {
                this.isModalKindsMessageVisible = false;
                this.close(); //close the ModalComponent too
            }
        },
        created() {
            console.log('ModalKindsComponent created.')
        },
        computed:{
            fills(){
                return this.fill();
            }
        }
    };
</script>
