<template>
  <main>
    <div>
      <h2 style="text-align: center; margin-top: 20px; margin-bottom: 20px; font-size: 40px;">Imágenes con Componente DataTable</h2>

      <DataTable :value="gatos" class="custom-datatable">
        <Column field="id" header="ID" class="costum-column"></Column>
        <Column  field="Nombre" header="Nombre" class="costum-column" :sortable="true" :filter="true" filterPlaceholder="Buscar por nombre"></Column>
        <Column header="Imagen" class="costum-column">
          <template #body="rowData">
            <img :src="rowData.data.Imagen" alt="" style="width: 200px; height: 200px;" />
          </template>
        </Column>
        <Column field="Atributo" header="Atributo" class="costum-column" :sortable="true" :filter="true" filterPlaceholder="Buscar por atributo"></Column>
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
  border-collapse: collapse;
  width: 100%;
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
        .get('https://ttnugkesbmrvaegysdgj.supabase.co/rest/v1/Gatos?apikey=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InR0bnVna2VzYm1ydmFlZ3lzZGdqIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDQ5Njg2MzMsImV4cCI6MjAyMDU0NDYzM30.o4Oy5cUqiyySiX0_F2Y5vI-bTPTPy51Y4KsZ56IljpM')
        .then(response => {
          this.gatos = response.data;
        })
        .catch(error => {
          console.error('Error al obtener datos de la API de gatos:', error);
        });
  },
};
</script>



