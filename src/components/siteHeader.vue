<template>
    <header class="bg-color ">
        <nav class=" container navbar navbar-expand-lg ">
            <div class="container">
                <router-link class="navbar-brand" to="/">
                    <img src="../assets/logo.png" alt="logo ulala" width="75" height="75" class="d-inline-block align-text-top">
                </router-link>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarScroll"
                    aria-controls="navbarScroll" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse justify-content-end" id="navbarScroll">
                    <ul class="navbar-nav text-center">
                        <li class="nav-item">
                            <router-link class="nav-link text-light" to="/">Inicio</router-link>
                        </li>
                        <li class="nav-item">
                            <router-link class="nav-link text-light" to="/productos">Productos</router-link>
                        </li>
                        <li class="nav-item">
                            <router-link class="nav-link text-light" to="/carrito">Carrito</router-link>
                        </li>

                    </ul>
                </div>
            </div>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'siteHeader'
}
</script>

<style scoped>

.bg-color{
    background-color: #d2b48c;
}
.navbar-brand{
    font-size: 2em; 
    color: black;  
    padding-bottom: 0.6rem;;
}
.navbar-brand:hover{
    color: black;
}
.nav-link{
    margin-right: 10px;
    margin-left: 10px;
    position: relative;
    color: rgb(43, 43, 43);
    transition: none; 
}
.nav-link:hover{
    color: rgb(0, 0, 0);
}
.nav-link::after{
    content: "";
    position: absolute;
    background-color: black;
    height: 3px;
    width: 0;
    left: 0;
    bottom: -3px;

}
.nav-link:hover:after{
    width: 100%;
    transition: .3s;
}
.navbar-expand-lg .navbar-nav .nav-link{
    font-weight: 550;
    font-size: 1.3em;
}

@media  screen and (max-width: 960px){
    .nav-link{
        border-top: rgba(141, 56, 52, 0.103) 1px solid;
        border-bottom: rgba(141, 56, 52, 0.103) 1px solid;
    }
    .nav-link:hover{
        background-color: #d2b48c;
        color: #f0f0f0;
    }
    .nav-link::after{
        content: none;
    }
}

</style>