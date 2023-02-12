<script setup>
 import { ref } from 'vue'
 defineProps (['inicio', 'fin', 'finPost'])
const emit = defineEmits(['next', 'prev'])


// se puede meter dentro de una constante los emit para evitar usar el emit dentro del boton
const next = () => {
  console.log('le diste click a next')
    emit('next')
}
const prev = () => {
  console.log('le diste click a prev')
    emit('prev')
}
</script>


<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" @click="prev" :disabled="inicio===0" class="btn btn-primary">Anterior {{ inicio }}</button>
        
        <button type="button" @click="next" :disabled="fin===finPost" class="btn btn-primary">Siguiente {{ fin }}</button>
      </div>
</template>