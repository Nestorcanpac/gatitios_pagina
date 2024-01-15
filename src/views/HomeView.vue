<template>
  <main>

    <a href="" class="btn btn-primary">Agregar</a>



    <div>
      <h2 style="text-align: center; margin-top: 20px; margin-bottom: 20px; font-size:40px;">Imagenes con Componente DataTable</h2>

      <DataTable :value="gatos" class="custom-datatable" >
        <Column field="id" header="ID" class="costum-column"  ></Column>
        <Column  header="URL" class="costum-column">
          <template #body="Paco">
            <img :src="`${Paco.data.url}`"  alt="" style="width: 300px; height: 300px;"/>
          </template>
        </Column>
        <Column field="width" header="Ancho" class="costum-column"></Column>
        <Column field="height" header="Altura"  class="costum-column"></Column>
      </DataTable>
    </div>
  </main>
</template>

<style>
DataTable {

}

.custom-datatable{
  border: 3px solid #181818 ;
  background-image: url("src/components/icons/GatoFondo.jpg");
}
.costum-column{
  border: 1px solid #181818;
  text-align: center;
  font-weight: bold;
  font-size: 40px
}

header{
  font-weight: bold ;
  text-align: center;
}

thead{
  font-weight: bold ;
  text-align: center;
}
.p-datatable-thead{
  font-weight: bold ;
  text-align: center;
}
thead.p-datatable-thead{
  font-weight: bold ;
  text-align: center;
}

</style>




<script>
import axios from 'axios';
import DataTable from "primevue/datatable";
import Column from "primevue/column";


export default {
  components: {
    DataTable,
    Column,
  },
  data() {
    return {
      gatos: [],
    };
  },
  mounted() {
    axios
        .get('https://api.thecatapi.com/v1/images/search?limit=10')
        .then(response => {
          this.gatos = response.data;
        })
        .catch(error => {
          console.error('Error al obtener datos de la API de gatos:', error);
        });
  },
};
</script>



