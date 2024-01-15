<script>
import axios from 'axios';
import Card from "primevue/card";

export default {
  components:{
    Card
  },


  data() {
    return {
      gatos: [],
    }
  },
  mounted() {
    axios.get('https://api.thecatapi.com/v1/images/search?limit=10')
        .then(response => {
          this.gatos = response.data;
        })
        .catch(error => {
          console.error('Error al obtener datos de la API de gatos:', error);
        });
  },
};
</script>

<template>
  <main>
    <div id="pacoco" style="margin: 0 auto; ">
      <h2 style="text-align: center; margin-top: 20px; margin-bottom: 20px; font-size:40px;">Imágenes de Gatos con Componente Card</h2>

      <div style="max-width: 100%; display: grid; justify-content: center">
        <card style="width: 25em; border: 1px solid #ddd; border-radius: 5px;" v-for="gato in gatos" :key="gato.id" class="Custom-Card">
          <template #title  >
            <span style="font-weight:bold;  font-size: 25px" class="custom_id">ID: </span>
            <span style=" font-size: 25px">{{ gato.id }}</span>
            </template>
          <template #subtitle>
            <span style="font-weight:bold; margin-left: 40px">Altura:</span> {{ gato.height }}  <span style="font-weight: bold" class="Custom-span">Ancho:</span> {{ gato.width }}</template>

          <template #footer>
            <Button icon="pi pi-check" label="Save" style="background-color: forestgreen; margin-left: 40px"  >Me gusta</Button>
            <Button icon="pi pi-times" label="Cancel"  style="background-color: red; margin-left:138px" >No me gusta</Button>
          </template>


          <template #content>
            <img :src="gato.url" :alt="'Gato ' + gato.id" style="width: 300px; height: 300px; margin-left: 40px" />
          </template>
        </card>

      </div>
    </div>
  </main>
</template>

<style>
element.style {
  max-width: 100%;
  display: grid;
  justify-content: center;
}
.Custom-Card{
  background-image: url("src/components/icons/GatoFondo.jpg");
  margin-bottom: 45px;
  font-weight: bold;
}

.Custom-span{
  margin-left: 140px;
}

.custom_id{
  margin-left: 145px;
}

#pacoco{
  max-width: 100%;
}

</style>

