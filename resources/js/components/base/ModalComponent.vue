<template>
    <transition name="modal-fade">
            <div class="modal">
                <div class="modal-background"></div>
                <div class="modal-card">
                    <header class="modal-card-head">
                        <p class="modal-card-title">Edit Entry</p>
                        <button class="delete" @click="close" aria-label="close"></button>
                    </header>
                    <section class="modal-card-body">
                        <!-- Content ... -->
                        <div class="columns is-multiline is-mobile">
                            <div class="column is-two-thirds"><input v-model="modal_name" class="input is-primary" type="text" key="spellSlug" placeholder="Spell Name"></div>
                            <div class="column is-2"><input v-model="modal_kind_id" class="input is-primary" type="text"  placeholder="Kind Id"></div>

                            <div class="column is-full"><input v-model="modal_quote" class="input is-primary" type="text"  placeholder="Spell Quote"></div>

                            <div class="column is-full"><textarea v-model="modal_description" class="textarea is-primary" type="text" placeholder="Spell Description"></textarea></div>
                        </div>

                    </section>
                    <footer class="modal-card-foot">
                        <button class="button is-primary" type="submit" v-on:click="update(modal_name, modal_quote, modal_description, modal_kind_id, modal_editSpells)">Save changes</button>
                        <button type="button" class="button is-primary" @click="fill" aria-label="Fill modal">Fill</button>
                        <button type="button" class="button is-primary" @click="close" aria-label="Close modal">Cancel</button>
                    </footer>
                </div>
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
    export default {
        name: 'ModalComponent',

        props: {
            name: {
                required: true,
                type: String
            },
            quote: {
                required: true,
                type: String
            },
            description: {
                required: true,
                type: String
            },
            kind_id: {
                required: true,
                type: String
            },
            slug:{
                required: true,
                type: String
            },
            editSpells:{
                required: true
            }


        },

        data() {
            return {
                modal_editSpells: {},
                modal_name: "",
                modal_quote:"",
                modal_description:"",
                modal_kind_id: "",
                modal_slug:"",
            }
        },
        methods: {
            close() {
                this.$emit('close');
            },
            fill(){
                this.modal_name = this.name
                this.modal_quote = this.quote
                this.modal_description = this.description
                this.modal_kind_id = this.kind_id
                this.modal_slug = this.slug
                this.modal_editSpells = this.editSpells
                console.log('Modal filled.')
            },
            update(name, quote, description, kind_id, editSpells) {
                axios
                    .put('/spell/'+ editSpells.slug, {name, quote, description, kind_id})
                    .then(({data}) => this.modal_editSpells = data);
                console.log('Update spells called.')
            },
        },
        created() {
            console.log('ModalComponent created.')
        },
    };
</script>
