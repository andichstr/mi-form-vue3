<template>
    <div class="container" v-if="usuarios.length != 0">
        <table class="table">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Nombre</th>
                    <th>Edad</th>
                    <th>Email</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, i) in usuarios" :key="item.id">
                    <td>{{i}}</td>
                    <td>{{item.nombre}}</td>
                    <td>{{item.edad}}</td>
                    <td>{{item.email}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    props: {
        usuarios: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
    .table{
        font-weight: bold;
    }

    .table > thead{
        background-color: #CB88B6;
    }

    .table > tbody{
        background-color: #B6CB88;
    }
</style>