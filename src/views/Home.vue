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
             
            
            ></v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-center">
            Hola - {{fecha}}  
          </v-card-text>
        </v-card>
      </v-col>
  
  </v-row>


</div>

  
</template>

<script>


export default {
  name: 'home', 
  data: () => {
    return {
      fecha : '', 
      fechaMinima : '2017',
      fechaMaxima : new Date().toISOString().substring(0,10)
    }
  }
  
}
</script>
