<template>
  <div>
    <h6 class="q-mb-none">Sistema operativo</h6>
    <q-list bordered separator>
      <q-item clickable v-ripple v-for="(sistema,key) in sistemas" :key="'Sis-'+key">
        <div>
        <q-checkbox v-model="sistema.value" />
        {{sistema.label}}<q-badge rounded color="orange" align="top">{{sistema.cantidad}}</q-badge>
      </div>
      </q-item>
    </q-list>
    <h6 class="q-mb-none">Marca</h6>
    <q-list bordered separator>
      <q-item clickable v-ripple v-for="(marca,key) in marcas" :key="'Mar-'+key">
        <div>
        <q-checkbox v-model="marca.value" />
        {{marca.label}}<q-badge rounded color="orange" align="top">{{marca.cantidad}}</q-badge>
      </div>
      </q-item>
    </q-list>
  </div>
  <h6 class="q-mb-none">Pantalla</h6>
    <q-list bordered separator>
      <q-item clickable v-ripple v-for="(panta,key) in pantallas" :key="'Pan-'+key">
        <div>
        <q-checkbox v-model="panta.value" />
        {{panta.label}}
      </div>
      </q-item>
    </q-list>
    <div>
        <q-btn @click="$emit('clickFiltro')" color="primary" icon="search" label="filtrar"/>
      </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'MenuFiltros',
  setup () {
    return {
      sistemas: ref([
        { value: false, label: 'Android', cantidad: 12 },
        { value: false, label: 'Ios', cantidad: 20 },
        { value: false, label: 'Windows', cantidad: 29 }]),
      marcas: ref([
        { value: false, label: 'Samsung', cantidad: 12 },
        { value: false, label: 'Huawei', cantidad: 10 },
        { value: false, label: 'Nokia', cantidad: 56 },
        { value: false, label: 'Iphone', cantidad: 4 },
        { value: false, label: 'Xiomi', cantidad: 4 }]),
      pantallas: ref([
        { value: false, label: '6.0' },
        { value: false, label: '5.5' },
        { value: false, label: '5' }])
    }
  }
}
</script>

<style>

</style>
