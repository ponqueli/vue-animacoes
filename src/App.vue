<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <div class="lead">Treinando transição/animação de elementos/componentes no Vue.</div>
      </div>
    </div>

    <div class="container">
        <h3 class="font-weight-light">Animações de Estado</h3> 
        <div class="form-group">
          <input class="form-control" v-model="numero" step="50">
        </div>

        <div class="alert alert-info">
            <h3 class="font-weight-light">
                <strong>Numero: </strong>
                <span>{{ numeroAnimado }}</span>
            </h3>
        </div>
      </div>
  </div>
</template>

<script>

import { gsap } from 'gsap'

export default {

  data(){
    return{
     numero: 0,
     numeroInterpolado: 0
    }
  },
  computed:{
    numeroAnimado(){
      return this.numeroInterpolado.toFixed(0)
    }
  },
  watch:{
      numero(novoNumero){
          gsap.to(this.$data, 2, { numeroInterpolado: novoNumero })
      }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu&display=swap');
#app{
  font-family: 'Ubuntu', sans-serif;
  width: 100%;
  height: 100%;
}
</style>
