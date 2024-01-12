<!--Single File Component-->
<script setup>
/* Single */
import { computed, ref } from 'vue';
const name = "Vue Dinamico";
const styleColor = "color:blue";
const arrayColores = ["blue", "red", "peru"];
const activo = false;
const arrayFrutas = ["🍎", "🍌", "🍓", "🍉", "🍒", "🍍"];
const objectArrayFrutas = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 20
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 5
  },
];
const objectFrutas = {
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana",
};
const arrNumeros = ref([]);

const handleClick = (message) => {
  alert(message);
}

const counter = ref(0); /* Variable Reactiva con Vue */

const increment = () => {
  counter.value++;
}
const decrease = () => {
  counter.value--;
}
const reset = () => counter.value = 0;
const add = () => {
  arrNumeros.value.push(counter.value)
}
const bloquearBtnAdd = computed(() => {
  const numSearch = arrNumeros.value.find((num) => num === counter.value)
  if(numSearch === 0)return true;
  return numSearch ? true : false;
  //return numSearch || numSearch === 0
})
/* Propiedades Computadas */
const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
});
</script>

<template>
  <!-- File -->
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <!-- Sintaxis de Plantilla <template></template> permite vincular declarativamente el DOM , {{ name }} interpolacion -->

  <h2>{{ arrayColores }}</h2>

  <!-- Enlaces de atributos -->
  <h2 :style="`color: ${arrayColores[2]}`">Soy Peru</h2>

  <!-- Expresiones JavaScript -->
  <!-- <h2>{{ activo ? "Estoy Activo":"Estoy Inactivo" }}</h2> -->

  <!-- Directivas,aplicar actualizaciones de forma reactiva al DOM -->
  <!-- v-if , v-else-if , v-else-->
  <h2 v-if="activo === true">Estoy Activo</h2>
  <!-- <h2 v-else>Estoy Inactivo</h2> -->
  <h2 v-else-if="activo === false">Estoy Inactivo</h2>
  <h2 v-else>Soy Elle</h2>

  <!-- v-show -->
  <h2 v-show="activo">Estoy Activo v-show</h2>

  <!-- v-for -->

  <h2>Array Frutas</h2>
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index"> {{ index }} - {{ fruta }}</li>
    <!--key se usa para señalar a vue la identidad de cada nodo-->
  </ul>

  <h2>Objeto en Array Frutas</h2>
  <ul>
    <li v-for="(fruta, index) in objectArrayFrutas" :key="index">{{ index }} - {{ fruta.name }} - {{ fruta.price }} - {{
      fruta.description }}</li>
  </ul>
  <h2>Recorriendo Propiedades</h2>
  <ul>
    <li v-for="(value, propiedad, index) in objectFrutas" :key="value">{{ index }} - {{ propiedad }} : {{ value }}</li>
  </ul>

  <!-- v-for y v-if , funciona casi como un while -->
  <h2>v-for y v-if</h2>
  <ul>
    <template v-for="item in objectArrayFrutas" :key="item.name">
      <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }}</li>
    </template>
  </ul>
  <!-- Eventos v-on @-->
  <div class="botones">
    <!-- Modificadores de Eventos -->
    <button v-on:click.right.prevent="handleClick('Boton Right')">Activame Right</button>
    <button @click.left="handleClick('Boton Left')">Activame Left</button>
    <button @click.middle="handleClick('Boton Middle')">Activame Middle</button>
  </div>

  <!-- Reactividad en vue -->
  <h2 :class="classCounter">{{ counter }}</h2>
  <!-- <h2 :class="counter > 0 ? 'positive' : 'negative'">{{ counter }}</h2> -->
  <!-- <h2 v-if="counter >= 0" :style="'color:green'">{{ counter }}</h2> -->
  <!-- <h2 v-else :style="'color:red'">{{ counter }}</h2> -->
  <!-- <h2 v-else-if="counter < 0" :style="'color:red'">{{ counter }}</h2> -->

  <div class="botones">
    <button @click="increment">Aumentar</button>
    <button @click="reset">Resetear</button>
    <button @click="decrease">Disminuir</button>
  </div>
  <button @click="add" :disabled="bloquearBtnAdd">Agregar</button>
  <br />
  {{ arrNumeros }}
  <ul>
    <li v-for="(num, index) in arrNumeros" :key="index">{{ num }}</li>
  </ul>
</template>

<style scoped>  /* Component */
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  h1 {
    color: red;
  }

  .botones {
    display: flex;
    justify-content: space-between;
  }

  .positive {
    color: green;
  }

  .negative {
    color: red;
  }

  .zero {
    color: peru;
  }
</style>
