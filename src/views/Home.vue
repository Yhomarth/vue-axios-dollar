<template>
<div>
    <v-row>
      <v-col  xs="12">
        <v-card>
          <v-date-picker 
            v-model="fecha"
            color="info"
            full-width
            :min="fechaMinima"
            :max="fechaMaxima"
            @change="getDollar(fecha)"
             
            
            ></v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-center">
            {{valor}} 
          </v-card-text>
        </v-card>
      </v-col>
  
  </v-row>


</div>

  
</template>

<script>


import {mapMutations} from 'vuex'
import axios from 'axios'
import moment from 'moment'


export default {
  name: 'home', 
  data: () => {
    return {
      fecha : moment().format("YYYY-MM-DD"), 
      fechaMinima : '2017',
      fechaMaxima : moment().format("YYYY-MM-DD"),
      valor : ''
    }
  }, 

  methods: {

    ...mapMutations(['mostrarLoading', 'ocultarLoading']),
   
   async getDollar(dia){
     
    
    let fechaArray = dia.split('-')
    let fechaFormat = fechaArray[2] + "-" + fechaArray[1] + "-" + fechaArray[0]     

     try {  
       this.mostrarLoading({titulo : 'cargando la informacion', color : 'secondary'})
        let datos = await axios.get(`https://mindicador.cl/api/dolar/${fechaFormat}`);
        this.valor =  await datos.data.serie[0].valor;       
     } catch (error) {
     this.valor =  'Sin resultados';       
     }
     finally{

       this.ocultarLoading()

     }
 
   }
   
  },

  created() {
 
    this.getDollar(this.fecha)
  }
  
}
</script>
