<template>
    <div :class="['card', cardColor]" class="m-2 pt-3 pb-3">
      <div class="card-body d-flex flex-column justify-content-between">
        <p class="card-title fw-bold fs-5">Paciente</p>
        <p>{{ cita.paciente }}</p>
        <p class="card-title fw-bold fs-5">Fecha</p>
        <p>{{ cita.fecha }}</p>
        <p class="card-title fw-bold fs-5">Hora</p>
        <p>{{ cita.hora }}</p>
        <p class="card-title fw-bold fs-5">Gravedad</p>
        <p>{{ cita.gravedad }}</p>
        <p class="card-title fw-bold fs-5">Motivo</p>
        <p>{{ cita.motivo }}</p>
        <button class="boton" @click="$emit('eliminar')">Eliminar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cita: Object
    },
    computed: {
      cardColor() {
        switch (this.cita.gravedad) {
          case 'Baja':
            return 'low';
          case 'Media':
            return 'medium';
          case 'Alta':
            return 'high';
          default:
            return 'bg-light';
        }
      }
    }
  };
  </script>
  
<style scoped>
  .low {
    background-color: green;
    color: white;
    .boton {
      background-color: rgb(255, 255, 255);
      padding: 5px 20px 5px 20px;
      border-radius: 10px;
      font-weight: bold;
      border: 1px solid green;
      color: green;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }
  }

  .medium {
    background-color: yellow;
    .boton {
      background-color: rgb(255, 255, 255);
      padding: 5px 20px 5px 20px;
      border-radius: 10px;
      font-weight: bold;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }
  }

  .high {
    background-color: rgb(141, 28, 0);
    color: white;
    .boton {
      background-color: rgb(255, 255, 255);
      padding: 5px 20px 5px 20px;
      border-radius: 10px;
      font-weight: bold;
      border: 1px solid rgb(141, 28, 0);
      color: rgb(141, 28, 0);
      display: block;
      margin-left: auto;
      margin-right: auto;
    }
  }

  .card-body {
    width: 300px;
  }
</style>
  