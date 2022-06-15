<template>
  <div id="app">
    <Formulario @agregar-usuario-tabla="agregarUsuarioTabla"/>
    <br><hr>
    <Tabla :usuarios="usuarios"/>
  </div>
</template>

<script>
import { ref } from 'vue'
import Formulario from './components/Formulario.vue'
import Tabla from './components/Tabla.vue'

export default {
    name: 'App',
    components: {
        Formulario,
        Tabla
    },
    setup() {
      const usuarios = ref([])
      return {
            usuarios
      }
    },
    methods: {
        agregarUsuarioTabla(usuario) {
            console.log(usuario);
            const nuevoUsuario = {...usuario};
            this.usuarios.push(nuevoUsuario);
        }
    }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
