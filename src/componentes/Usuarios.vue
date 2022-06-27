<template>
  <section class="src-componentes-usuarios">
    <div class="jumbotron">
      <h1>usuarios</h1>
      <hr />
      <br />
      <button class="btn btn-warning mr-3" @click="getXHR()">
        Get USers XHR
      </button>
      <button class="btn btn-success mr-3" @click="getFetch()">
        Get Users Fetch
      </button>
      <button class="btn btn-success mr-3" @click="getAxios()">
        Get Users Axios
      </button>
      <button class="btn btn-danger my-3" @click="usuarios = []">CLEAR</button>


      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>id</th>
            <th>nombre</th>
            <th>email</th>
            <th>telefono</th>
          </tr>
          <tr v-for="(usuarios, index) in usuarios" :key="index">
            <td>{{ usuarios.id }}</td>
            <td>{{ usuarios.nombre }}</td>
            <td>{{ usuarios.email }}</td>
            <td>{{ usuarios.telefono }}</td>
          </tr>
        </table>
        <h5 class="alert alert-primary text-center">
          Se encontraron {{ usuarios.length }} usuarios.
        </h5>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encontraron Usuarios
      </h4>
    </div>


  </section>
</template>

<script>
export default {
  name: "src-componentes-usuarios",
  props: [],
  mounted() {},
  data() {
    return {
      url: "https://62b8e721ff109cd1dc89476f.mockapi.io/users",
      usuarios: []
    };
  },
  methods: {
    getXHR() {
      const xhr = new XMLHttpRequest();
      xhr.open("get", this.url);
      xhr.addEventListener("load", () => {
        if (xhr.status == 200) {
          let respuesta = JSON.parse(xhr.response);
          /* console.log(respuesta); */
          this.usuarios = respuesta;
        } else {
          console.error("ERROR XHR (status)", xhr.status);
        }
      });
      xhr.addEventListener("error", (e) => {
        console.error("ERROR XHR", e);
      });
      xhr.send();
    },

    async getFetch() {
      try {
        let response = await fetch(this.url);
        let respuesta = await response.json();
        this.usuarios = respuesta;
      } catch (error) {
        console.error("Error Fetch", error);
      }
    },

    async getAxios() {
      try {
        let { data } = await this.axios(this.url);
        this.usuarios = data;
      } catch (error) {
        console.error("Error Axios", error);
      }
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.src-componentes-usuarios {
}
</style>
