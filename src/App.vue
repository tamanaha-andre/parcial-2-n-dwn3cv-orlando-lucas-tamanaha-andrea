<template>
  <div>
    <siteHeader></siteHeader>
    <router-view
      :productos="productos" @evento="(id) => agregarCarrito(id)"
      @eliminar="(index) => eliminarCarrito(index)"
      @productoEditado="(producto) => editar(producto)"
      @productoNuevo="(producto) => agregar(producto)"
      :carrito="carrito"
      :total="total"
      :cantidad="cantidad">
    </router-view>
  </div>
</template>

<script>
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap-icons/font/bootstrap-icons.css"
import siteHeader from "./components/siteHeader.vue";

export default {
  name: "App",
  components: {
    siteHeader,
    
  },

  methods: {
    agregarCarrito: function (productoid) {

      if (this.carrito.length != 0) {
       
        let bandera = false;

     
        this.carrito.forEach((item) => {
          if (item.id == productoid) {
            bandera = true;
            item.cantidad++;
            let objStr = JSON.stringify(this.carrito);
            localStorage.setItem("productos", objStr);
          }
        });

        if (bandera == false) {
          this.carrito.push({
            id: productoid,
            titulo: this.productos[productoid].titulo,
            precio: this.productos[productoid].precio,
            imagen: this.productos[productoid].imagen,
            img_alt: this.productos[productoid].img_alt,
            cantidad: 1,
          });

          let objStr = JSON.stringify(this.carrito);
          localStorage.setItem("productos", objStr);
        }

        bandera = false;
     
        if (this.carrito.length > 0) {
          this.total = 0;
          this.cantidad = 0;
          this.carrito.forEach((item) => {
            this.total += item.precio * item.cantidad;
            this.cantidad += item.cantidad;
          });

      
          localStorage.setItem("total", JSON.stringify(this.total));
          localStorage.setItem("cantidad", JSON.stringify(this.cantidad));
        }
      } else {

     
        this.carrito.push({
          id: productoid,
          titulo: this.productos[productoid].titulo,
          precio: this.productos[productoid].precio,
          imagen: this.productos[productoid].imagen,
          img_alt: this.productos[productoid].img_alt,
          cantidad: 1,
        });

    
        let objStr = JSON.stringify(this.carrito);
        localStorage.setItem("productos", objStr);

        
        if (this.carrito.length > 0) {
          this.total = 0;
          this.cantidad = 0;
          this.carrito.forEach((item) => {
            this.total += item.precio * item.cantidad;
            this.cantidad += item.cantidad;
          });

      
          localStorage.setItem("total", JSON.stringify(this.total));
          localStorage.setItem("cantidad", JSON.stringify(this.cantidad));
        }
      }
    },
    eliminarCarrito: function(i){
 
      console.log(`Total:${this.total} = ${this.carrito[i].precio} * ${this.carrito[i].cantidad}`);

      this.total -= (this.carrito[i].precio * this.carrito[i].cantidad);
      localStorage.setItem('total', JSON.stringify(this.total));

      this.cantidad -= this.carrito[i].cantidad;
      localStorage.setItem('cantidad', JSON.stringify(this.cantidad));

      this.carrito.splice(i,1);
      localStorage.setItem('productos', JSON.stringify(this.carrito));

    },
    editar: function(producto){
      this.productos[producto.producto_id].titulo = producto.titulo;
      this.productos[producto.producto_id].producto_cat = producto.producto_cat;
      this.productos[producto.producto_id].precio = producto.precio;
      this.productos[producto.producto_id].imagen = producto.imagen;
      this.productos[producto.producto_id].img_alt = producto.img_alt;
    },
    agregar: function(producto){
      this.productos.push({
        producto_id: producto.producto_id,
        titulo: producto.titulo,
        producto_cat: producto.producto_cat,
        precio: producto.precio,
        imagen: producto.imagen,
        img_alt: producto.img_alt,
      });
    }

  },

  created() {
    this.carrito = localStorage.getItem("productos") ? JSON.parse(localStorage.getItem("productos")) : [];
    this.total = localStorage.getItem("total") ? JSON.parse(localStorage.getItem("total")) : [];
      this.cantidad = localStorage.getItem("cantidad") ? JSON.parse(localStorage.getItem("cantidad")) : [];
  },

  data() {
    return {
      carrito: [],
      total: 0,
      cantidad: 0,
     
        productos: [
        {
                producto_id: 1,
                cat_producto: 1,
                destacado: true,
                titulo: "Blusa Rosa Blei",
                precio: 9500,
                imagen: require("../src/assets/blu01.jpg"),
                alt_img: "Blusa de escote con volados volant"
            },
            {
                producto_id: 2,
                cat_producto: 1,
                titulo: "Blusa Capri",
                precio: 7000,
                imagen: require("@/assets/blu02.jpg"),
                alt_img: "Blusa amarilla calada y cuello solapa."
            },
            {
                producto_id: 3,
                cat_producto: 1,
                titulo: "Blusa Constance",
                precio: 9500,
                imagen: require("../src/assets/blu03.jpg"),
                alt_img: "Blusa blanca calada y escote redondo."
            },
            {
                producto_id: 4,
                cat_producto: 1,
                titulo: "Camisa Gandha Sounds",
                precio: 8200,
                imagen: require("../src/assets/blu04.jpg"),
                alt_img: "Blusa negra, escote en pico y calada."
            },
            {
                producto_id: 5,
                cat_producto: 2,
                destacado: true,
                titulo: "Vestido azul bordada",
                precio: 10500,
                imagen: require("../src/assets/ves01.jpg"),
                alt_img: "Vestido azul bordado en hilo oro y mangas media."
            },
            {
                producto_id: 6,
                cat_producto: 2,
                titulo: "Vestido Ikat",
                precio: 12500,
                imagen: require("../src/assets/ves02.jpg"),
                alt_img: "Vestido corto liso de broderie con mangas largas."
            },
            {
                producto_id: 7,
                cat_producto: 2,
                titulo: "Vestido Plain",
                precio: 11300,
                imagen: require("../src/assets/ves03.jpg"),
                alt_img: "Vestido corto liso de broderie con mangas largas."
            },
            {
                producto_id: 8,
                cat_producto: 3,
                titulo: "Vestido corto Niran",
                precio: 9600,
                imagen: require("../src/assets/ves04.jpg"),
                alt_img: "Vestido corto estampado, con mangas babuchas."
            },
            {
                producto_id: 9,
                cat_producto: 3,
                destacado: true,
                titulo: "Bote Negra",
                precio: 4200,
                imagen: require("../src/assets/rem01.jpg"),
                alt_img: "Remera bote negra"
            },
            {
                producto_id: 10,
                cat_producto: 3,
                destacado: true,
                titulo: "Remera alas",
                precio: 3900,
                imagen: require("../src/assets/rem02.jpg"),
                alt_img: "Remera espampa vuelo."
            },

            {
                producto_id: 11,
                cat_producto: 3,
                destacado: true,
                titulo: "Remera blanca",
                precio: 2300,
                imagen: require("../src/assets/rem03.jpg"),
                alt_img: "Remera canela."
            },

            {
                producto_id: 12,
                cat_producto: 3,
                destacado: true,
                titulo: "Remera calada",
                precio: 2300,
                imagen: require("../src/assets/rem04.jpg"),
                alt_img: "Remera canela calada."
            },

        ],
    };
  },
};
</script>

<style>
 * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .titulo {
    font-size: 2.5rem;
    font-weight: 700;
  }
  .subtitulo {
    font-size: 1.3rem;
    color: rgba(0, 0, 0, 0.7);
  }
  .btn0{
      height: 40px;
      width: 40%;
      outline: none;
      border: none;
      background-color: #d2b48c;
      border-bottom: solid #2c2811;
      color: white;
      border-radius: 60px;
      font-weight: 700;
  }

  .btn1 {
    display: inline-block;
    margin: 20px;
    padding: 10px 0;
    text-align: center;
    height: 45px;
    width: 35%;
    border: none;
    outline: none;
    text-decoration: none;
    background-color: #d2b48c;
    color: white;
    font-weight: 700;
    border-radius: 60px;
    transition: 0.5s;
  }
  .btn0:hover,
  .btn1:hover,
  .btn3:hover {
    background-color: #d2b48c;
    color: white;
  }
  .btn3 {
    display: inline-block;
    margin: 20px 20px 20px 0px;
    padding: 10px 0;
    text-align: center;
    height: 45px;
    width: 35%;
    border: none;
    outline: none;
    text-decoration: none;
    background-color: #2c2811;
    color: white;
    font-weight: 700;
    border-radius: 60px;
  }

  .button {
    border: none;
    border-radius: 20px;
    cursor: pointer;
    font-size: 1.3rem;
    font-weight: 600;
    margin: 5px;
    padding: 0.5rem 1rem;
    text-align: center;
    text-decoration: none;
    transition: all 0.3s ease;
  }

  .card{
    border-radius: 20px;
     box-shadow: 0 10px 29px 0 rgb(68 88 144 / 10%);
     transition: 0.5s;
  }

  .card-body{
    padding: 0;
    overflow: hidden;
  }

  .card-body picture{
   overflow: hidden;
  }
  .card-body img{
    border-radius: 20px 20px 0 0;
    transform: scale(1);
    transition: all ease .3s

  }

  .card-body:hover img{
   transform: scale(1.1);
  }

  .card-body a{
    text-decoration: none;
  }

  .card-body a h5, .card-body a p{
    margin: 0;
    padding-left: 20px;
    padding-right: 20px;
    color: #343a40;
    text-decoration: none !important;
  }

  .card-body h5{
   padding-top: 20px !important;
  }

  .precio{
    font-weight: 800;
    padding-bottom: 30px;
    padding-top: 20px;
    font-size: 28px;
    color: #2c2811 !important
  }

  .btn-color{
   background-color:  #d2b48c;
   color: white;
   border-radius: 20px;
   transition: .5s all ease;
  }
  .btn-color:hover{
   background-color: #d2b48c ;
   color: white;
  }


</style>

