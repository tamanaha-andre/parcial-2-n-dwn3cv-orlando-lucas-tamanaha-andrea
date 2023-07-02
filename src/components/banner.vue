<template>
          
    <section class="banner-home">

        <h1 class="visually-hidden">Inicio</h1>

        <div id="carouselExampleFade" class="carousel slide carousel-fade" data-bs-ride="carousel">
            <div class="carousel-inner">
                <div class="carousel-item active">
                    <img src="../assets/banner.jpg" class="d-block w-100" alt="banner camisas">
                </div>
                <div class="carousel-item">
                    <img src="../assets/banner-dos.jpg" class="d-block w-100" alt="banner cueros">
                </div>
                <div class="carousel-item">
                    <img src="../assets/banner-tres.jpg" class="d-block w-100" alt="banner new-in">
                </div>
            </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleFade" data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleFade" data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div>
        
    </section>

</template>

<script>
export default {
    name: 'banner',
}
</script>
<style scoped>

    .banner{   
    background-size: cover;
    height: 40vh;
    background-position: 50% 50%;
    width: 100%;
    }
    .banner h2{
        font-size: 4rem;
        font-weight: 400;
        color: white;
    }

    @media screen and (max-width: 768px){
        .banner{
            height: 100vh;
        }
    }
</style>