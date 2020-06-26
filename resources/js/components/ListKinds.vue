<template>
    <div>
        <div class="container is-fluid">

            <h1 class="title is-3 is-spaced" >List of all Kinds</h1>
            <div class="table-container" >
                <table class="table is-striped is-hoverable table-hover">
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
                        <tr v-for="kinds in listKinds" :key="kinds.id" v-on:dblclick="showModal(kinds)">
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
        </div>

        <ModalKindsComponent
            v-show="isKindsModalVisible"
            @close="closeModal"
            :description="this.modal_description"
            :name = "this.modal_name"
            :slug = "this.modal_slug"
            :editKinds = "this.editKinds"
        />

    </div>
</template>

<script>
    import ModalKindsComponent from "./base/ModalKindsComponent";

    export default {
        components: {
            ModalKindsComponent,
        },
        mounted() {
            console.log('Component mounted.')
        },
        data() {
          return {
              name: "",
              description: "",
              editKinds: {},
              listKinds: {},

              isKindsModalVisible: false,
              modal_name: '',
              modal_description: '',
              modal_slug:''
          }
        },
        created() {
            axios.get('./list/kind')
            .then(({data}) => this.listKinds = data);
            console.log('List kinds created.')
        },

        methods: {
            showModal(kinds) {
                this.modal_name = kinds.name
                this.modal_description = kinds.description
                this.modal_slug = kinds.slug
                this.editKinds = kinds
                this.isKindsModalVisible = true
                console.log('showKindsModal called.')
            },
            closeModal() {
                this.isKindsModalVisible = false;
            },
        }
    };
</script>
