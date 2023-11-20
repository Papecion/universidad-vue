<template>
    <div class="container">
      <h1>Listado de carreras</h1>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Id</th>
            <th scope="col">Nombre</th>
            <th scope="col">Descripción</th>
            <th scope="col">Duración (años)</th>
            <th scope="col">Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(carrera, index) in carreras" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ carrera.nombre }}</td>
            <td>{{ carrera.descripcion }}</td>
            <td>{{ carrera.duracion_anios }}</td>
            <td>
              <!-- Agrega aquí los botones de acciones si es necesario -->
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>

<script>
import axios from 'axios';

export default {
  name: 'Carrera',
  data() {
    return {
      carreras: [],
    };
  },
  mounted() {
    axios
      .get('http://127.0.0.1:8000/api/carreras')
      .then(response => (this.carreras = response.data.carreras))
      .catch(error => console.error('Error al obtener las carreras:', error));
  },
};
</script>