<template ref="articulosPrincipales">
  <div class="row justify-center ">
<div class="col-4 row q-pt-md ">
  <div class="col">
    <q-btn :ripple="false" @click="cargarArticulos" v-show="hayfiltro" color="secondary" label="Limpiar filtro" no-caps />
  </div>
  Precio:
  <q-input rounded class="col" standout bottom-slots v-model.number="desde" label="Desde"  dense type="number">
        <template v-slot:prepend>
          <q-icon name="attach_money" />
        </template>

      </q-input>
      <q-input  class="col" rounded standout bottom-slots v-model.number="hasta" label="Hasta"  dense type="number">
        <template v-slot:prepend>
          <q-icon name="attach_money" />
        </template>

      </q-input>
      <div>
        <q-btn @click="filtrarPrecio" round color="primary" icon="search" />
      </div>

</div>
      <q-select outlined v-model="ordernarPor" :options="opcionesOrdenar" label="Ordenar por" dense class="col-7 mobile-only " @update:model-value="cambioSelectorOrdenar"/>
<div class="col-5 desktop-only q-ma-md" >
  ordenar por:
      <q-btn-toggle
      de
        v-model="ordernarPor"
        class="my-custom-toggle "
        no-caps
        rounded
        unelevated
        toggle-color="primary"
        color="white"
        text-color="primary"
        :options="opcionesOrdenar"
        @click="ordenarArticulo"

      />
</div>
  </div>
  <div class="row ">
   <!-- <q-card class="my-card col-4">
      <img src="https://cdn.quasar.dev/img/mountains.jpg">

      <q-card-section>
        <div class="text-h6">Our Changing Planet</div>
        <div class="text-subtitle2">by John Doe</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-btn to="/articulo/434324234" label="index" outline color="purple" />
      </q-card-section>
    </q-card> -->
    <q-card class="my-card col-6 q-pa-sm col-md-3" v-for="(card,key) in articulos" :key="key">
      <img src="https://cdn.quasar.dev/img/mountains.jpg">

      <q-card-section>
        <div class="text-h6">{{card.precio}}</div>
        <div class="text-subtitle2">{{card.titulo}}</div>
      </q-card-section>

      <q-card-section class="q-pt-none" >
        <q-btn :to="'/articulo/'+ card.id" label="index" outline color="purple" />
      </q-card-section>
    </q-card>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const ordernarPor = ref('PRECIO')
const opcionesOrdenar = ref([
  { label: 'PRECIO', value: 'PRECIO' },
  { label: 'FECHA', value: 'FECHA' }])
const articulosOriginales = [
  { id: 'asdaddsdas1', precio: 20.25, titulo: 'Iphone 6 pantalla de 8 pulgadas, 64Gb internos,2Gb de Ram, Sólo Banda Tigo, Nuevo', vendedor: 'JuaN Perez', telefono: '3124124142-23231', fecha: '2022-10-05' },
  { id: 'asdaddsdas2', precio: 26.25, titulo: 'Iphone 5 pantalla de 8 pulgadas, 64Gb internos,2Gb de Ram, Sólo Banda Tigo, Nuevo', vendedor: 'JuaN Perez', telefono: '3124124142-23231', fecha: '2022-10-05' },
  { id: 'asdaddsdas3', precio: 24.25, titulo: 'Iphone 7 pantalla de 8 pulgadas, 64Gb internos,2Gb de Ram, Sólo Banda Tigo, Nuevo', vendedor: 'JuaN Perez', telefono: '3124124142-23231', fecha: '2022-10-05' },
  { id: 'asdaddsdas4', precio: 28.25, titulo: 'Iphone 4 pantalla de 8 pulgadas, 64Gb internos,2Gb de Ram, Sólo Banda Tigo, Nuevo', vendedor: 'JuaN Perez', telefono: '3124124142-23231', fecha: '2020-10-05' }]
const articulos = ref([])
const desde = ref(0)
const hasta = ref(0)
const hayfiltro = ref(false)
// computed
// const hayfiltroprecio = computed(() => {
//   if (desde.value > 0 && hasta.value > 0) { return true } else { return false }
// })
// odservador
// watch(hayfiltroprecio, (newX) => {
//   console.log(newX)
// })
// metodos
function filtrarPrecio () {
  hayfiltro.value = true
  if (desde.value > 0 && hasta.value > 0) {
    articulos.value = articulos.value.filter((item) => {
      if (item.precio >= desde.value && item.precio <= hasta.value) { return true } else { return false }
    })
  }
}
function cambioSelectorOrdenar (value) {
  console.log('entro')
  ordernarPor.value = value.value
  ordenarArticulo()
}
function ordenarArticulo () {
  if (ordernarPor.value === 'PRECIO') {
    articulos.value.sort((a, b) => a.precio - b.precio)
  }
  if (ordernarPor.value === 'FECHA') {
    articulos.value.sort(function (a, b) {
      if (a.fecha > b.fecha) {
        return 1
      }
      if (a.fecha < b.fecha) {
        return -1
      }
      // a must be equal to b
      return 0
    })
  }
}
function cargarArticulos () {
  hayfiltro.value = false
  articulos.value = []
  articulosOriginales.forEach(item => {
    articulos.value.push(item)
  })
  ordenarArticulo()
}
// ciclo de vida
onMounted(() => {
  cargarArticulos()
})
</script>
