<template>

  <div class="d-flex justify-content-between mt-3">

    <div class="d-flex">

      <input
        v-model="filtro"
        class="px-2 search"
        type="search"
        placeholder="Buscar"
        aria-label="Search"
      />
      <button @click="$emit('filtrar', buscar(productos))" class="btn0" type="button" value="Buscar">Buscar</button>
    
    </div>

    <div>                
      
      <select @change="$emit('filtrar', buscar(productos))" v-model="categoria" class="form-select" name="Categorias">
         
          <option value="4" selected>Ver Todos</option>
          <option value="1">Blusas</option>
          <option value="2">Vestidos</option>
          <option value="3">Remeras</option>
      </select>
    </div>

  </div>

</template>

<script>
  export default {
    name: 'catalogoBuscador',
    props: {
      productos:Array
    },
    methods: {
      buscar: function(productos){

        // Filtro por precio o por categoria
        switch (this.categoria) {
          case '3':

            productos = productos.sort((a, b) => {
              if (a.precio > b.precio) {return 1};
              if (a.precio < b.precio) {return -1};
              return 0;
            })
            
          break;

          case '4':

            productos = productos;
            
          break;
        
          default:
            
            productos = productos.filter(producto => producto.producto_cat == this.categoria);
          
          break;

        }

        // Filtro con Buscador
        if ((productos.length > 0) && (!this.filtro == '')) {

          productos = productos.filter(producto => producto.titulo.toLowerCase().includes(this.filtro.toLowerCase()));

        }else if(!this.filtro == ''){
          productos = productos.filter(producto => producto.titulo.toLowerCase().includes(this.filtro.toLowerCase()));
        }

        return productos;
      }
    },
    data() {
      return {
          filtro: '',
          categoria: 5,
      };
    },
  };
</script>

<style scoped>
  .search{
      height: 40px;
      width: 100%;
      border-radius: 60px;
      outline: none;
      margin-right: -35px;
      border: 2px #d2b48c;
  }
</style>