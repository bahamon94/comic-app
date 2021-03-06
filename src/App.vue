<template>
<div class="flex items-center justify-center bg-yellow-600 p-7">
  <div class="max-w-3xl p-4 bg-white border border-gray-200 rounded-xl">
    <h1 class="block mt-3 text-3xl font-semibold leading-snug text-center text-black ">
      Woodpecker
    </h1>
    <img class="mt-2 border border-gray-100 rounded-2xl" src="https://imgs.xkcd.com/comics/woodpecker.png"/>
    <div class="my-1 border border-b-0 border-gray-200"></div>
    <div class="mt-3 text-gray-500">
      <Rating  :calificacion="calificacion" @seleccion-calificar="generarCalificacion" />
    </div>
  </div>
</div>
</template>

<script>
import { onBeforeUnmount, onMounted, reactive, toRefs, watch } from '@vue/runtime-core';
import Rating from "./components/component_Rating";
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Rating
  },
  setup(){
    onBeforeUnmount(() => { document.body.className = 'home' })

    const state = reactive({
      calificacion: 0,
      srcImageComic : ''
    })

    function generarCalificacion(value) {
      if (typeof value.cantidad === 'number' && value.cantidad <= value.max && value.cantidad >= 0 ) {
        state.calificacion = state.calificacion === value.cantidad ? value.cantidad -1 : value.cantidad
      }

    }

     function traerInfoComic(numeroComic) {
     let headers = { "mode": "no-cors" };

      
      const request = new Request(`https://xkcd.com/${numeroComic}/info.0.json`, headers)
      
     fetch(request).then( response => Cache.put(request, response) )
      // let { title, img } = await comic.json()
      //  
      
    }

    onMounted(() => generarAleatorio())

   async function generarAleatorio() {
      let numeroComic =( Math.random()*1000).toFixed()
      let respuesta  = await traerInfoComic(numeroComic)
      console.log(respuesta);
    }

    // watch(
    //   () => state.numeroComic,
    //   () => traerInfoComic()
    // )

   return { ...toRefs(state), generarCalificacion }
  }
 
}
</script>

<style lang="scss">
</style>
