<template>
  <main>
        <section class="shop app">
            <div class="container">
                <div class="row py-5">
                    <div class="col-lg-8 m-auto text-center mb-5">
                        <h1 class="titulo">ulala</h1>
                        <h2 class="subtitulo mb-5">Tu Tienda OnLine</h2>                        
                    </div>
                    
                    <div class="row">
                        <div class="col-md-3 text-center mb-4" v-for="(producto, index) in productos" :key="producto.id">
                            <div class="card border-0 bg-light mb-2 shadow">
                                <div class="card-body">
                                    <a href="#">
                                     <picture>
                                        <img v-bind:src="producto.imagen" class="w-100" :alt="producto.img_alt"></picture>

                                        <div class="descripcion px-4">

                                        <h3 class="h4 pt-4">{{producto.titulo}}</h3>
                                        <p class="precio">${{producto.precio.toLocaleString('ES-AR')}}</p>
                                        </div>
                                    </a>

                                    <div class="container">
                                     <div class="row">
                                        <div class="col-12">
                                        <button @click="$emit('evento', producto.producto_id)" class="btn button btn-carrito w-100"><i class="bi bi-cart-plus"></i> Agregar al carrito</button>
                                        </div>
                                        <div class="col-6">
                                        <button v-on:click="editar(index)" class="btn btn-outline-success button w-100"><i class="bi bi-pencil-square"></i></button>
                                        </div> 
                                        <div class="col-6">
                                            <button v-on:click="eliminar(index)" class="btn btn-outline-danger button w-100"><i class="bi bi-trash"></i></button>
                                        </div> 
                                     </div>
   
                                    </div>
                                </div>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

</template>

<script>
    import catalogoBuscador from '../components/catalogoBuscador.vue'
    
    export default {
        name: 'catalogoView',
        components: {
            catalogoBuscador,
        },
        computed: {
            productosFinales() {
                return this.productosNuevos.length > 0 ? this.productosNuevos : this.productos;
            },
        },
        props: {
            productos: Array
        },
        methods: {
            editar: function(index){
                this.form = true;
                this.productoEditar = this.productos[index];
            },
        },
        data() {
            return {
                form: false,
                productoEditar: {},
                productosNuevos: [],
            };
        },

    }
    
</script>

<style scoped>
    a{
        color: black;
        text-decoration: none;
    }
    .h4{
        font-size: 1.25rem;
        font-weight: bolder;
        margin: 5px 0 0 0;
    }
    .btn-carrito{
        background-color: #d2b48c;
        color: white;
        transition: all ease .3s;
    }

    .btn-carrito:hover{
        background-color: #d2b48c ;
    }
    
</style>