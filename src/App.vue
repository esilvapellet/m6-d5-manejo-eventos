<template>
  <div id="app" class="container">
    <h1 class="text-center fw-bold my-3">Registro de atenciones clínicas</h1>
    <hr />
    <section
      id="formIngreso"
      class="border border-1 border-secondary rounded m-5"
    >
      <form class="col my-4" @submit.prevent="agregarPaciente">
        <div class="d-flex justify-content-around">
          <div class="col-2 mx-3">
            <label
              for="paciente"
              class="form-label"
              :class="{ inactivo: !datosPaciente.nombre }"
              >Nombre paciente</label
            >
            <hr />
            <input
              type="text"
              id="paciente"
              class="form-control"
              v-model="datosPaciente.nombre"
            />
          </div>
          <div class="col-2 mx-3">
            <label
              for="fecha"
              class="form-label"
              :class="{ inactivo: !datosPaciente.fecha }"
              >Fecha</label
            >
            <hr />
            <input
              type="date"
              id="fecha"
              class="form-control"
              v-model="datosPaciente.fecha"
            />
          </div>
          <div class="col-2 mx-3">
            <label
              for="hora"
              class="form-label"
              :class="{ inactivo: !datosPaciente.hora }"
              >Hora</label
            >
            <hr />
            <input
              type="time"
              id="hora"
              class="form-control"
              v-model="datosPaciente.hora"
            />
          </div>
          <div class="col-2 mx-3">
            <label
              for="gravedad"
              class="form-label"
              :class="{ inactivo: !datosPaciente.gravedad }"
              >Nivel de gravedad</label
            >
            <hr />
            <select
              class="form-select"
              id="gravedad"
              v-model="datosPaciente.gravedad"
            >
              <option v-for="(gravedad, index) in nivelGravedad" :key="index">
                {{ gravedad }}
              </option>
            </select>
          </div>
          <div class="col-2 mx-3">
            <label
              for="motivo"
              class="form-label"
              :class="{ inactivo: !datosPaciente.motivo }"
              >Motivo de consulta</label
            >
            <hr />
            <input
              type="text"
              id="motivo"
              class="form-control"
              v-model="datosPaciente.motivo"
            />
          </div>
        </div>
        <div class="text-center p-3">
          <button class="btn btn-dark px-3" :disabled="!btnActivo">
            Agregar atención <i class="fa-regular fa-circle-check"></i>
          </button>
        </div>
      </form>
    </section>
    <section class="container">
      <p
        class="textoRojo text-center container"
        v-if="listaPacientes.length < 1"
      >
        No se han registrado consultas.
      </p>
      <hr />
      <div class="row row-cols-lg-6 g-2 justify-content-evenly">
        <CardPaciente
          v-for="(paciente, index) in listaPacientes"
          :key="index"
          :style="colorCard(paciente.gravedad)"
          :nombre="paciente.nombre"
          :fecha="paciente.fecha"
          :hora="paciente.hora"
          :motivo="paciente.motivo"
          @eliminarPaciente="listaPacientes.splice(index, 1)"
        />
      </div>
    </section>
  </div>
</template>

<script>
import CardPaciente from "./components/CardPaciente.vue";

export default {
  name: "App",
  components: {
    CardPaciente,
  },
  data() {
    return {
      nivelGravedad: ["Baja", "Media", "Alta"],
      datosPaciente: {
        nombre: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },
      listaPacientes: [],
    };
  },
  methods: {
    agregarPaciente: function () {
      const nuevoPaciente = Object.assign({}, this.datosPaciente);
      this.listaPacientes.push(nuevoPaciente);
      this.datosPaciente = {
        nombre: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
    },
    colorCard: function (gravedad) {
      if (gravedad === "Baja") {
        return "background-color : #94ddaf;";
      } else if (gravedad === "Media") {
        return "background-color: #d8db8e;";
      } else if (gravedad === "Alta") {
        return "background-color: #db9090";
      }
    },
  },
  computed: {
    btnActivo: function () {
      return (
        this.datosPaciente.nombre &&
        this.datosPaciente.fecha &&
        this.datosPaciente.hora &&
        this.datosPaciente.gravedad &&
        this.datosPaciente.motivo
      );
    },
  },
};
</script>

<style>
body {
  font-family: "Noto Sans", sans-serif;
  background-image: url("./assets/background.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-color: black;
}
#formIngreso {
  background-color: #ffffff;
  /* opacity: 0.5; */
}
.inactivo {
  color: #af0f0f;
}
.textoRojo {
  color: #af0f0f;
}
</style>