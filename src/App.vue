<template>
  <div id="app">
    <FormularioWeb @datosIngresados="mostrarTabla" />
    <TableData :datos="datos" v-if="mostrarTabla" />
  </div>
</template>

<script>
import { ref } from 'vue';
import FormularioWeb from './components/FormularioWeb.vue';
import TableData from './components/TableData.vue';

export default {
  components: {
    FormularioWeb,
    TableData
  },

  setup() {
    const datos = ref([]); 
    const mostrarTabla = ref(false);

    const mostrarTablaHandler = (datosIngresados) => {
      datos.value.push(datosIngresados);
      mostrarTabla.value = true;
    };

    return {
      datos,
      mostrarTabla,
      mostrarTablaHandler,
    };
  },
};
</script>

