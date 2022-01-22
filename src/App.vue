<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <div class="lead">Treinando transição/animação de elementos/componentes no Vue.</div>
      </div>
    </div>

    <div class="container">
       <div class="form-group">
        <select name="animacoes" id="selectAnimacoes" class="form-control" v-model="animacaoSelecionada">
          <option value="fade">Fade</option>
          <option value="zoom">Zoom</option>
          <option value="slide">Slide</option>
        </select>
      </div>

      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>

      <!-- 2 Elementos diferentes dentro do transition com if e else funcionam, mas com 2 divs ou seja 2 elementos iguais, o vue precisa de uma key pra saber q sao 2 elementos diferentes-->
      <transition :name="animacaoSelecionada" mode="out-in">
        <div class="alert alert-info" v-if="mostrar" key="info"> Animações no Vue (informação)</div>
        <div class="alert alert-success" v-else key="success"> Animações no Vue (success)</div>
      </transition>

      <!--Java Script Hooks-->
      <!-- <transition 
        appear

        @before-enter="beforeEnter"
        @enter="enter"
        @after-enter="afterEnter"
        @enter-cancelled="enterCancelled"

        @before-leave="beforeLeave"
        @leave="leave"
        @after-leave="afterLeave"
        @leave-cancelled="leaveCancelled"
        
        :css="false"

        >
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition> -->

      <!--https://animate.style -->
      <!-- <transition 
        appear
        appear-class=""
        appear-active-class="animate__animated animate__flipInY"
        appear-to-class=""

        enter-class=""
        enter-active-class="animate__animated animate__zoomInDown"
        enter-to-class=""

        leave-class=""
        leave-active-class="animate__animated animate__hinge"
        leave-to-class=""
        >
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition> -->

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
       mostrar: true,
       animacaoSelecionada: 'fade'
     }
   },
   methods:{
     beforeEnter(el){
      console.log("BeforeEnter ")
      el.style.opacity = 0
     },
     enter(el, done){
      console.log("enter "+el)
      let contagem = 0
      const intervalo = setInterval(()=>{
        el.style.opacity = + el.style.opacity + 0.1
        contagem++
        if(contagem > 10 ){
          clearInterval(intervalo)
          done()
        }
      }, 150 )

     },
     afterEnter(el){
       console.log("afterEnter "+el)
     },
     enterCancelled(el){
       console.log("enterCancelled "+el)
     },

      beforeLeave(el){
        console.log("beforeLeave ")
        el.style.transition = 'width 0.5s'
        el.style.overflow = 'hidden'
        el.style.whiteSpace = 'nowrap'
      },
      leave(el, done){
        console.log("Leave ")
        let contagem = 0
        const tamanho = el.offsetWidth

        const intervalo = setInterval(()=>{
          el.style.width = (tamanho * (1 - (contagem / 10))) + 'px'
          contagem++

          if( contagem > 10 ){
            clearInterval(intervalo)
            done()
          }
        }, 150 )
      },
      afterLeave(el){
        console.log("afterLeave "+el)
      },
      leaveCancelled(el){
        console.log("LeaveCancelled "+el)
      },
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
    transition: opacity 0.7s;
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
