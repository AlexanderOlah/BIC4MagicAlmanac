<template>
    <div>
        <h1>Create Kinds Component</h1>
        <table class="table table-hover">
            <tbody>
            <tr>
                <th>name:</th>
                <td><input type="text" id="name-kind" name="name-kind"></td>
            </tr>
            <tr>
                <th>description</th>
                <td><input type="text" id="description-kind" name="description-kind"></td>
            </tr>
            </tbody>
        </table>

        <button id="create-kind" name="create-kind">Create Kind</button>
        <!--
              <div class="content" hidden id="created-Kind">
            <table class="table table-hover">
                <tbody>
                <tr>
                    <th>id:</th>
                    <td>{{kinds.id}}</td>
                </tr>
                <tr>
                    <th>slug:</th>
                    <td>{{kinds.slug}}</td>
                </tr>
                <tr>
                    <th>name:</th>
                    <td>{{kinds.name}}</td>
                </tr>
                <tr>
                    <th>description:</th>
                    <td>{{kinds.description}}</td>
                </tr>
                <tr>
                    <th>created at:</th>
                    <td>{{kinds.created_at}}</td>
                </tr>
                <tr>
                    <th>updated at</th>
                    <td>{{kinds.updated_at}}</td>
                </tr>
                </tbody>
            </table>
        </div>
        -->


    </div>
</template>

<script>
    const kind = document.getElementById('create-kind');
    addEventListener('click',kind);

    function createKind() {

    axios.post('./kind', {name: document.getElementById("name-kind"),
        description: document.getElementById("description-kind")})
}
</script>
