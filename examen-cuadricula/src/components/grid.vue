<template>
<div>
 <div class="container-grid">
  <div 
      class="items" 
      v-for="(imagen , index) in imagenes" :key="imagen.id"
      
   >

     <button 
        class="btn" 
        @click="borrar(index)" 
        >

     <td class="titles">{{imagen.title}}</td>

     <img 
     class="img"
     :src="imagen.url" 
     :alt="imagen.title">

     </button>
   </div>
 </div>
</div>
  
</template>

<script>
import axios from 'axios';

export default {
  name: 'Grid',
  
  components: {
    
  },
  data(){
    return {
      imagenes: null,
      }
  },
  mounted(){
    this.getTodos();
  },
  computed: {

  },
  methods: {
    getTodos(){
      //realizamos la llamada a nuestra API para poder traer el contenido.
      axios.get('https://jsonplaceholder.typicode.com/photos')
           .then(res =>{
             //cargamos en imagenes el resultado del data para luego poder utilizarlo.
            this.imagenes = res.data;  
        }
           )},

    borrar(index){
       this.imagenes.splice(index, 1)
    }
  }
}

</script>

<style scoped>


.container-grid{
   display: grid;
   grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
   row-gap: 5.5em;
   padding: 3em;
   background-color: cadetblue

   }
  .items{
    background: white ;
    height: 300px;
    width: 300px
  }

  .btn{
    border: none;
    cursor: pointer;
  }

  .btn:hover{
    background-color: lightgray

    }

  .titles{
    font-size: 15px;
    height: 70px;
    padding: 5px
  } 
   

</style>