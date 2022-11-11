<template>
  <q-page class="">
   <h4>hola</h4>
   {{$route.params.idArticulo}}

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ArticuloMostrar'
})
</script>
