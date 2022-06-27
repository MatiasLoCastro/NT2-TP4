<template>
  <section class="src-componentes-formulario">
    <div class="div jumbotron">
      <h2>Componente FormularioAv</h2>
      <hr />
      <hr />
      <br />

      <vue-form :state="formState" @submit.prevent="enviar()">
        <!-- Campo Nombre -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            name="nombre"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />
          <!-- Mensajes de validacion -->
          <field-messages name="nombre" show="$dirty">
            <div class="alert alert-success mt-1">Success!</div>
            <div
              v-if="formState.$dirty"
              slot="required"
              class="alert alert-danger mt-1"
            >
              Campo no valido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere minimo {{ nombreMinLength }} caracteres
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- Campo edad -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Edad</label>
          <input
            type="number"
            id="edad"
            name="edad"
            class="form-control"
            autocomplete="off"
            v-model.number="formData.edad"
            required
            :min="edadMin"
            :max="edadMax"
          />
          <!-- Mensajes de validacion -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad minima permitida es de {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad maxima permitida es de {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- Campo email -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Email</label>
          <input
            type="email"
            id="email"
            name="email"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.email"
            required
          />
          <!-- Mensajes de validacion -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="email" class="alert alert-danger mt-1">
              Email no valido
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- Boton envio -->
        <button class="btn btn-success my-4" :disabled="formState.$invalid">
          Submit
        </button>
      </vue-form>
      <div v-if="users.length" class="table-responsive">
        <table class="table table-dark">
           <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(user, index) in users" :key="index">
            <td>{{ user.nombre }}</td>
            <td>{{ user.edad }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encontraron usuarios.
      </h4>

      <!-- <hr />
      <p><u>formData</u></p>
      <pre>{{ formData }}</pre>

      <hr />
      <p><u>formState</u></p>
      <pre>{{ formState }}</pre> -->
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 5,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
      users: [],
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: "",
        edad: "",
        email: "",
      };
    },
    enviar() {
      this.users.push({ ...this.formData });
      console.log({ ...this.formData });
      this.formData = this.getInitialData(); //Reset de los datos del vue-form
      this.formState._reset(); // reset de los estados del vue-form
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: purple;
  color: white;
}

hr {
  background-color: #bbb;
}

pre {
  color: white;
}
</style>
