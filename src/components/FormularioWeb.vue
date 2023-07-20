<template>
    <div class="container app">
      <h2 class="mt-4 mb-4 text-center">Ingresa tus datos</h2>
      <form @submit.prevent="submitForm">
        <div>
          <label for="nombre">Nombre:</label>
          <input class="form-control" type="text" id="nombre" v-model="formulario.nombre">
          <div>
            <span v-if="errors.nombre" class="error">{{ errors.nombre }}</span>
          </div>
        </div>
        <br>
        <div>
          <label for="apellido">Apellido:</label>
          <input class="form-control" type="text" id="apellido" v-model="formulario.apellido">
          <div>
            <span v-if="errors.apellido" class="error">{{ errors.apellido }}</span>
          </div>
        </div>
        <br>
        <div>
          <label for="edad">Edad:</label>
          <input class="form-control" type="number" id="edad" v-model="formulario.edad">
          <div>
            <span v-if="errors.edad" class="error">{{ errors.edad }}</span>
          </div>
        </div>
        <br>
        <div>
          <label for="email">Email:</label>
          <input class="form-control" type="email" id="email" v-model="formulario.email">
          <div>
            <span v-if="errors.email" class="error">{{ errors.email }}</span>
          </div>
        </div>
        <br>
        <button class="btn btn-primary" type="submit">Enviar</button>
      </form>
  
      <table class="table table-bordered border border-info-subtle border-4 mt-5">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody v-if="datos.length > 0">
          <tr v-for="item in datos" :key="item.id">
            <td>{{ item.nombre }}</td>
            <td>{{ item.apellido }}</td>
            <td>{{ item.edad }}</td>
            <td>{{ item.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'; 
  
  export default {
    setup() {
      const formulario = ref({
        nombre: '',
        apellido: '',
        edad: '',
        email: '',
      });
      const errors = ref({});
      const datos = ref([]);
  
      const submitForm = () => {
        if (validateForm()) {
          const newData = { ...formulario.value };
          newData.id = Date.now();
          datos.value.push(newData);
          resetForm();
        } else {
          console.log('Formulario inválido. Por favor, verifica los campos.');
        }
      };
  
      const validateForm = () => {
        errors.value = {};
  
        if (!formulario.value.nombre) {
          errors.value.nombre = 'El campo Nombre es obligatorio.';
        }
  
        if (!formulario.value.apellido) {
          errors.value.apellido = 'El campo Apellido es obligatorio.';
        }
  
        if (!formulario.value.edad) {
          errors.value.edad = 'El campo Edad es obligatorio.';
        } else if (isNaN(formulario.value.edad)) {
          errors.value.edad = 'El campo Edad debe ser un número.';
        }
  
        if (!formulario.value.email) {
          errors.value.email = 'El campo Email es obligatorio.';
        } else if (!isValidEmail(formulario.value.email)) {
          errors.value.email = 'Por favor, ingresa un email válido.';
        }
  
        return Object.keys(errors.value).length === 0;
      };
  
      const isValidEmail = (email) => {
        const emailRegex = /\S+@\S+\.\S+/;
        return emailRegex.test(email);
      };
  
      const resetForm = () => {
        formulario.value.nombre = '';
        formulario.value.apellido = '';
        formulario.value.edad = '';
        formulario.value.email = '';
      };
  
      return {
        formulario,
        errors,
        datos,
        submitForm,
      };
    },
  };
  </script>
  
  <style scoped>
  
  .app {
    width: 50%;
    margin: 0 auto;
  }
  
  table, thead {
    width: 50% !important;
    margin: 0 auto;
  }
  .btn-primary {
    width: 47ch;
  }
  
  .error {
    color: red;
  }
  </style>
  
