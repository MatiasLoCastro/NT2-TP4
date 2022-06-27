<template>
  <div id="app">
    <Formulario />
    <Usuarios/>
  </div>
</template>

<script>
import Formulario from "./componentes/Formulario.vue";
import Usuarios from './componentes/Usuarios.vue'

export default {
  name: "App",
  components: {
    Formulario,
    Usuarios,
  },
};
</script>

<style>

</style>
