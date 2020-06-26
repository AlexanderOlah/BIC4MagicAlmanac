<template>
    <div class="container is-fluid">
        <h1 class="title is-3 is-spaced">Search Spells by Keyword</h1>

        <div class="columns is-multiline is-mobile">
            <div class="column is-half"><input v-model="q" v-on:input="query(q)"  type="text" class="input is-primary" placeholder="Spell Name"></div>
        </div>
        <div class="table-container">
            <table class="table is-striped is-hoverable table-hover">
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
                    <tr v-for="spells in searchSpells" :key="spells.id" v-on:dblclick="showModal(spells)">
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

        <ModalComponent
            v-show="isModalVisible"
            @close="closeModal"
            :description="this.modal_description"
            :kind_id="this.modal_kind_id"
            :name = "this.modal_name"
            :quote = "this.modal_quote"
            :slug = "this.modal_slug"
            :editSpells = "this.editSpells"
            @open="ModalComponent.fill()"
        />

    </div>
</template>

<script>
    import ModalComponent from "./base/ModalComponent";
    export default {
        components: {
            ModalComponent,
        },
        name: "SearchSpells",
        mounted() {
            console.log('Component mounted.')
        },
        data() {
            return {
                searchSpells: {},
                editSpells: {},
                q: "",
                name: "",
                quote:"",
                description:"",
                kind_id: "",

                isModalVisible: false,
                modal_name: '',
                modal_quote: '',
                modal_description: '',
                modal_kind_id: '',
                modal_slug:''
            }
        },
        created() {
            },
        computed: {
            showSuccessMessage() {
                return this.successMessage !== '';
            }
        },

        methods: {
            query(q) {
                axios
                    .post('/search/spell', {q})
                    .then(({data}) => this.searchSpells = data);
                console.log('Search spells called.')
            },
            showModal(spells) {
                this.modal_name = spells.name
                this.modal_quote = spells.quote
                this.modal_description = spells.description
                this.modal_kind_id = spells.kind_id
                this.modal_slug = spells.slug
                this.editSpells = spells
                this.isModalVisible = true
                console.log('showModal called.')
            },
            closeModal() {
                this.isModalVisible = false;
            },
        }
    }
</script>
