<script setup>
import { productos } from "./datos"
import { ref, computed } from "vue"

const contador = ref(0)

const ruta = "https://www.html6.es/img/rey_"

const totalElementos = productos.length;

const next = () => {
  contador.value++

  if (contador.value >= totalElementos) {
    contador.value = 0
  }
}

const rey = computed(() => {
  const nombre = productos[contador.value].nombre.toLowerCase()
  return nombre.substring(0, 1).toUpperCase() + nombre.substring(1);
})

const imagen = computed(() => {
  return ruta + productos[contador.value].nombre.toLowerCase() + ".png";
})

const nuevoPrecio = computed(() => {
  return Number(productos[contador.value].precio / 1.10).toFixed(2);
})

</script>

<template>
  <div class="container">
    <div>
      <h2>Cena {{ contador + 1 }}
        con el rey godo {{ rey }}
      </h2>

      <h3 class="precio">Precio: {{ productos[contador].precio }}$</h3>

      <div>
        <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Solo fines de semana)</div>
        <div v-else class="todosLosDias dias">(De lunes a domingo)</div>
      </div>

      <div v-if="productos[contador].precio < 100" class="oferta">
        <div>Ahorra un 10% dto:
          {{ nuevoPrecio }}$
        </div>

        <img src="../public/oferta.jpg" alt="">
      </div>

      <img :src="imagen" alt="">
      <br>
      <button @click="next">Siguiente ({{ contador + 1 }} / {{ totalElementos }})</button>
    </div>
  </div>
</template>

<style scoped>
* {
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

button {
  cursor: pointer;
  background-color: gray;
  border-radius: 10px;
  border: none;
  padding: 5px;
}

.oferta {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  text-align: center;
}

div .todosLosDias {
  background-color: green;
}

.soloFinesDeSemana {
  background-color: red;
}

.dias {
  display: inline-block;
  color: white;
  padding: 4px 17px;
  font-size: 0.9m;
  border-radius: 4px;
  margin: 5px 0 10px;
  display: inline-block;
}

.oferta img {
  width: 65px;
}
</style>
