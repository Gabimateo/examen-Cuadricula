<template>
<div>
 <div class="container-grid">
   <div class="items" v-for="image in imagenes" :key="image.id">
     <td class="titles">{{image.title}}</td>
     <img 
     class="img"
     :src="image.url" 
     alt="photo">
     
   </div>
 </div>
</div>
  
</template>

<script>
import axios from 'axios'
export default {
  name: 'Grid',

  data(){
    return {
      imagenes:null,
      }
  },
  mounted(){
    this.getTodos();
  },
  methods: {
    getTodos(){
      axios.get('https://jsonplaceholder.typicode.com/photos')
           .then(response =>{
             this.imagenes = response.data;
             console.log(this.imagenes)
           })
           .catch(e=>
             console.log(e)
           )
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
   background-color: darkgray

   }
  .items{
    background: white ;
    height: 300px;
    width: 300px
  }
  .titles{
    font-size: 15px;
    height: 70px;
    padding: 5px
  } 
   

</style>