<template>
    <div>
        <h1>Create Kinds Component</h1>
        <table class="table table-hover">
            <tbody>
            <tr>
                <th>name:</th>
                <td><input type="text" id="nameKind"></td>
            </tr>
            <tr>
                <th>description:</th>
                <td><input type="text" id="descriptionKind"></td>
            </tr>
            </tbody>
        </table>

        <button id="createKind">Create Kind</button>
        <button id="Name">Create Name</button>
        <button id="Desc">Create Describe</button>
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

    const bt = document.getElementById('createKind');
    if(bt) {
        bt.addEventListener('click', createKind);
    }
    function createKind() {
    axios.post('./kind', {name: document.getElementById("nameKind"),
        description: document.getElementById("descriptionKind")});
    console.log('After Post kinds created.');
    }
</script>
