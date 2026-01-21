<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import { ref, reactive } from 'vue'
import BotonContador from './components/BotonContador.vue';

const mensaje = ref("Esto es un mensaje")
const contador = ref(1);
const visible = ref(true);
const riesgos = ['alto', 'medio', 'bajo'];
const miRiesgo = ref('bajo');
const objeto = {
  propiedad1: 4,
  propiedad2: "texto",
  propiedad3: true,
  propiedad4: [3, 6, 3, 4, 7]
}

const cliente = reactive({
  nombre: "Andrés",
  sueldo: 5000
})

const numeros = reactive([]);
const nuevoNumero = ref(0);

const cambiarMensaje = () => {
  alert("otra cosa");
  mensaje.value="otra cosa"
}

const cambiarRiesgo = (nuevoRiesgo) => miRiesgo.value = nuevoRiesgo;

const caracteristicas = reactive(['fuerza', 'habilidad', 'vida', 'magia']);

function borrarCaracteristica(index) {
  caracteristicas.splice(index,1);
}
</script>

<template>
  <h1>Esta es mi primera app con vue</h1>
  <p>El mensajes es: {{ mensaje }}</p>  
  <button @click="cambiarMensaje">Cambiar mensaje</button>  
  <button @click="contador++">{{ contador }}</button>
  <button @click="visible=!visible">{{ visible ? "Está visible" : "No está visible" }}</button>
  <p>{{ visible }}</p>
  <p v-if="visible">Esto es porque esta visible</p>
  <p v-else>Cuando no es visible se muestra esto</p>
  <h3 v-if="contador>10">El contador pasa de 10</h3>
  <p>
    <label for="">Cambiar mensaje: </label>
    <input type="texto" v-model="mensaje">
  </p>
  <ul>
    <li v-for="(riesgo,index) in riesgos" 
      :key="index"
      :class="riesgo"
      @click="miRiesgo=riesgo"
      @mouseover="cambiarRiesgo(riesgo)"
    >
      {{ riesgo }}
    </li>
  </ul>
  <p :class="miRiesgo">Mi riesgo es {{ miRiesgo }}</p>
  <select v-model="miRiesgo" :class="miRiesgo">
    <option v-for="(riesgo,index) in riesgos" 
      :key="index" 
      :class="riesgo"
      :value="riesgo">{{ riesgo }}</option>
  </select>
  <p>Tengo un objeto: {{ objeto }}</p>
  <ul>
    <li>Propiedad1: {{ objeto.propiedad1 }}</li>
    <li>Propiedad2: {{ objeto.propiedad2 }}</li>
    <li>Propiedad3: {{ objeto.propiedad3 }}</li>
    <li>Propiedad4, elemento 3: {{ objeto.propiedad4[3] }}</li>
  </ul>
  <h3>Cliente</h3>
  <p>
    Nombre: {{ cliente.nombre }} -
    <input type="text" v-model="cliente.nombre">
  </p>
  <p>
    Sueldo: {{ cliente.sueldo }} - 
    <input type="number" v-model="cliente.sueldo">
  </p>
  <h3>Números</h3>
  <p>{{ numeros }}</p>
  <p>Insertar nuevo número:
    <input type="number" v-model="nuevoNumero"
      @keypress.enter="numeros.push(nuevoNumero)"
    >
    <button @click="numeros.push(nuevoNumero)">Insertar</button>
  </p>
  <BotonContador titulo="fuerza" />

  <BotonContador titulo="energía"/>
  <BotonContador titulo="vida"/>
  
  <ul>
    <li v-for="(caracteristica,index) in caracteristicas" :key="index" >
      <BotonContador :titulo="caracteristica" @borrarCaracter="borrarCaracteristica(index)"/>
    </li>
  </ul>
</template>

<style scoped>
  .alto {
    color: red;
  }

  .medio {
    color: orange;
  }

  .bajo {
    color: green;
  }
</style>
