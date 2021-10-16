<template>
  <div class="container-total">
    <h1>Prueba Grid Responsive/reactiveJS</h1>
    <div class="container-grid">
      <div class="items" v-for="(imagen, index) in imagenes" :key="imagen.id">
        <button class="btn" @click="borrar(index)">
          <img class="img" :src="imagen.url" :alt="imagen.title" />
        </button>
      </div>
      
      <!-- aqui es donde llamamos a la dependencia
       que nos permite hacer un scroll infinito, 
       haciendo nuevas llamadas a la API a 
       medida que vamos haciendo scroll -->

      <infinite-loading @infinite="getTodos"></infinite-loading> 
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import InfiniteLoading from 'vue-infinite-loading';

export default {
  name: 'Grid',
  
  components: {
    InfiniteLoading
  },
  data(){
    return {
      imagenes: '',
      limit:15
      }
  },
  methods: {
    getTodos($state){
          //realizamos la llamada a nuestra API para poder traer el contenido            
               axios.get('https://jsonplaceholder.typicode.com/photos')
           .then(res =>{
             //verificamos que existan registros que traer.
             if(res.data.length){
               //sumamos de 5 en 5 el limite de registros que traemos desde la API.
            this.limit +=5;
             //cargamos en imagenes el resultado del data para luego poder utilizarlo.
            this.imagenes = res.data.splice(0, this.limit)
            //si hay registros los cargamso sino, el estado pasa a estar completo.
            $state.loaded()
             }else{
               $state.complete()
             }
        }
        );    
    },
    borrar(index){
       this.imagenes.splice(index, 1)
    },
    }
  }

</script>

<style scoped>
.container-total {
  height: 100%;
}
.container-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
  column-gap: 0.5em;
  row-gap: 2em;
  padding: 3em;
  background-color: cadetblue;
  width: 100%;
}
.items {
  height: 100%;
  width: 100%;
}
.items:hover {
  padding-top: 10px;
  padding-left: 10px;
  height: 195px;
  width: 95%;
}

.btn {
  border: none;
  cursor: pointer;
}

.titles {
  font-size: 15px;
  height: 70px;
  padding: 5px;
}
@media (max-width: 1280px){
 .container-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
 }
 }
@media (max-width: 1000px){
 .container-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
 }
 }
@media (max-width: 800px){
 .container-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
 }
 }
@media (max-width: 500px){
 .container-grid {
  display: grid;
  grid-template-columns: 1fr;
 }
 }

</style>