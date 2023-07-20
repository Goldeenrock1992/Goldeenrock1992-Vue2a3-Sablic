<template>
    <div>
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dato, index) in datos" :key="index">
            <td>{{ dato.nombre }}</td>
            <td>{{ dato.apellido }}</td>
            <td>{{ dato.edad }}</td>
            <td>{{ dato.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
    
  export default {
    props: {
      datos: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    padding: 8px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }
  
  th {
    background-color: #f2f2f2;
  }
  </style>

