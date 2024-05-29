<template>
  <div class="cardPaciente col-3 m-3">
    <div class="text-center p-3 card-body">
      <h6 class="text-start">Nombre paciente:</h6>
      <hr />
      <p>{{ nombre }}</p>
      <h6 class="text-start">Fecha:</h6>
      <hr />
      <p>{{ fecha }}</p>
      <h6 class="text-start">Hora:</h6>
      <hr />
      <p>{{ hora }}</p>
      <h6 class="text-start">Motivo de consulta</h6>
      <hr />
      <p>{{ motivo }}</p>
      <button class="btn textoRojo" @click="$emit('eliminarPaciente')">
        Cancelar <i class="fa-regular fa-trash-can"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardPaciente",
  props: {
    nombre: String,
    fecha: String,
    hora: String,
    motivo: String,
  },
};
</script>

<style scoped>
.cardPaciente {
  border-radius: 15px;
}
.textoRojo {
  background-color: #af0f0f;
  color: #ffffff;
}
</style>