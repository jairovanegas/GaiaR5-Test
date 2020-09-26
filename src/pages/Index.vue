<template>
  <q-page>
    <div class="row">
      <div class="col-8">
        <q-select
          filled
          v-model="tags"
          multiple
          :options="opciones"
          label="Tags"
          style="width: 250px"
          class="full-width"
        />
      </div>
      <div class="col-4">
        <q-btn label="Buscar" icon="search" @click="filtrar" color="orange" glossy class="full-width"/>
      </div>
    </div>
    <div class="row full-width">
      <q-list bordered separator class="full-width">
        <q-item v-for="(centro, indice) in centrosAcopioFiltrados" :key="'centro'+centro.nombre+indice">
          <q-item-section>
            <centro-acopio-busqueda :centro="centro"/>
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import CentroAcopioBusqueda from "components/CentroAcopioBusqueda.vue";
import CentroAcopio from "../api/clases/CentroAcopioBusqueda";

@Component({
  components: { CentroAcopioBusqueda }
})
export default class PageIndex extends Vue {
  tags:String[] = [];
  opciones: String[] = ['Plastico', 'Vidrio', 'Madera', 'Carton', 'Metal', "Pizza"];
  centrosAcopio: CentroAcopio[] = [
    new CentroAcopio(
      "Las marianas",
      "Calle 100 #89-15",
      ["Plastico", "Madera"],
      "8:00 am a 5:00 pm",
      "search"
    ),
    new CentroAcopio(
      "Los hermanos de javier",
      "Calle 45 #7-30",
      ["Metal", "Vidrio"],
      "9:00 am a 10:00 pm",
      "add"
    ),
    new CentroAcopio(
      "El codito",
      "Calle 13 #30-20",
      ["Plastico", "Madera", "Vidrio", "Carton"],
      "8:00 am a 5:00 pm",
      "delete"
    ),
    new CentroAcopio(
      "Las tortugas",
      "Calle 69 #4-20",
      ["Pizza"],
      "10:00 pm a 8:00 am",
      "wifi"
    )
  ];
  centrosAcopioFiltrados: CentroAcopio[] = [];

  filtrar(){
    this.centrosAcopioFiltrados = [];
    this.tags.forEach((tag)=>{
      this.centrosAcopio.forEach((centro)=>{
        if(centro.tags.some((tagCentro)=>{
          if(!this.centrosAcopioFiltrados.includes(centro) && tag == tagCentro){
            this.centrosAcopioFiltrados.push(centro);
            return true;
          }
        }));
      })
    })
  }
};
</script>
<style>

</style>
