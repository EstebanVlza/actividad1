<template>
  <h2>Cena {{contador + 1}}
    con el rey godo {{ rey }}
  </h2>
  <h3 class="precio">Precio:${{ productos[contador].precio }}</h3>
  <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Solo fines de semana)</div>
  <div v-else class="dias todosLosDias">(De lunes a domingo)</div>
  <div v-if="productos[contador].precio<100" class="oferta">
    <div>Ahora un 10% dto:
      ${{ nuevoPrecio }}</div>
      <img src="/src/assets/oferta.jpg" alt="rey godo en descuento"/>
  </div>
  <img :src="imagen" class="king"/>

  <button @:click="siguiente">Siguiente ({{contador + 1}}/ {{ total }})</button>

</template>

<script setup>
  import {ref,computed} from "vue"
  import {productos} from "./datos.js"
  const contador=ref(0)
  const total= productos.length;
  const ruta="https://www.html6.es/img/rey_";
  const siguiente=()=>{
    contador.value++
    if (contador.value>=total){
      contador.value=0;
    }
  }
  const rey=computed(()=>{
    const elNombre=productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0,1).toUpperCase() + elNombre.substring(1)
  })
  const imagen=computed(()=>{
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
  })
  const nuevoPrecio=computed(()=>{
    return Number(productos[contador.value].precio/1.10).toFixed(2)
  })
</script>

<style scoped>
.todosLosDias{
  background-color: green;
}
.soloFinesDeSemana{
  background-color: red;
}
.dias{
  color:white;
  padding:4px 17px;
  font-size: 0.9em;
  border-radius: 4px;
  margin:5px 0 10px;
  display: inline-block;
}
.king {
  height: 300px;
}
</style>