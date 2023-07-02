<template>
  <main>
    <banner/>
    <tarjetas :productos="productosDestacados"/>
  </main>
</template>

<script>


import banner from '@/components/banner.vue'
import tarjetas from '@/components/tarjetas.vue'

export default {
  name: 'inicioView',
  components: {
    banner,
    tarjetas,
  },
  props: {
    productos: {
      type: Array,
      required: true
    }
  },

  computed: {
    productosDestacados() {
      return this.productos.filter((producto) => producto.destacado);
    },
  },

}
</script>
