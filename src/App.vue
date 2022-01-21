<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="dsplay-4">Animações</h1>
        <div class="lead">Treinando transição/animação de elementos/componentes no Vue.</div>
      </div>
    </div>

    <div class="container">
      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>
      <!--https://animate.style -->
      <transition 
        enter-class=""
        enter-active-class="animate__animated animate__zoomInDown"
        enter-to-class=""

        leave-class=""
        leave-active-class="animate__animated animate__hinge"
        leave-to-class=""
        >
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition>

      <!-- <transition name="fade">
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition>

      <transition name="zoom">
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition>

      <transition name="slide" type="animation" :duration="{ enter: 1200, leave: 500 }">
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition> -->
    </div>

  </div>
</template>

<script>

export default {
   data(){
     return{
       mostrar: true
     }
   }
}
</script>

<style>
  body{
    overflow: hidden;
  }
</style>

<style scoped>
 
  .slide-enter, .slide.leave-to{
    opacity: 0;
  }
  .slide-enter-active{
    animation: slide 0.7s;
    transition: opacity 0.7s;
  }
  
  .slide-leave-active{
    animation: slide 0.7s reverse;
    transition: opacity 2s;
  }

  @keyframes slide {
    0% {
      transform: translateX(-100px);
    }
    100% {
      transform: translateX(0px);
    }
  }

  /*zoom */
  .zoom-enter, .zoom-leave-to{
    transform: scale(0);
  }
  .zoom-enter-active, .zoom-leave-active{
    transition: transform 0.5s;
  }
  
  /*fade */
 /*Entrada */
 /*Estado inicial */
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }
  .fade-enter-active, .fade-leave-active{
    transition: opacity 1s;
  }
</style>
