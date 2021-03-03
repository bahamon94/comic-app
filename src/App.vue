<template>
  <Rating  :calificacion="calificacion" @seleccion-calificar="generarCalificacion" />
</template>

<script>
import { onBeforeUnmount, reactive, toRefs } from '@vue/runtime-core';
import Rating from "./components/component_Rating";

export default {
  name: 'App',
  components: {
    Rating
  },
  setup(){
    onBeforeUnmount(() => { document.body.className = 'home' })

    const state = reactive({
      calificacion: 0
    })

    function generarCalificacion(value) {
      if (typeof value.cantidad === 'number' && value.cantidad <= value.max && value.cantidad >= 0 ) {
        state.calificacion = state.calificacion === value.cantidad ? value.cantidad -1 : value.cantidad
      }

    }

   return { ...toRefs(state), generarCalificacion }
  }
 
}
</script>

<style lang="scss">
</style>
