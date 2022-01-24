<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <div class="lead">Treinando transição/animação de elementos/componentes no Vue.</div>
      </div>
    </div>

    <div class="container">

      <h3 class="font-weight-light">Tecnologias</h3> 
      <div class="row">
        <div class="col-sm-10">
          <div class="form-group">
            <input 
              type="text"
              class="form-control"
              placeholder="Insira um novo item e pressione Enter"
              @keyup.enter="adicionar"
              ref="input">
          </div>
        </div>
      </div>

      <transition-group tag="ul" class="list-group" name="list">
        <li 
          class="list-group-item"
          v-for="(tecnologia, indice) in tecnologias"
          :key="tecnologia">
          <span> {{ tecnologia }} </span>
          <button 
            class="btn btn-danger btn-sm float-right"
            @click="remover(indice)"
            >X
          </button>
        </li>
      </transition-group>

      <div class="col-sm-2 mt-3 pl-0">
        <button class="btn btn-info" @click="embaralhar">Embaralhar</button>
      </div>
    </div>
  </div>
</template>

<script>

import { shuffle } from 'lodash'

export default {

  data(){
    return{
      tecnologias:[
        'JavaScript',
        'Vue JS',
        'Vuex',
        'Vue Router'
      ]
    }
  },
  methods:{
    adicionar(event){
      const novoItem = event.target.value
      if(novoItem){
        const indice = Math.floor(Math.random() * this.tecnologias.length)
        this.tecnologias.splice(indice, 0, novoItem)
        this.$refs.input.value = ''
      }
    },
    remover(indice){
      this.tecnologias.splice(indice, 1)
    },
    embaralhar(){
      this.tecnologias = shuffle(this.tecnologias)
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

.list-enter, .list-leave-to{
  opacity: 0;
  transform:  translateX(-70px);
}

.list-enter-active, .list-leave-active, .list-move{
  transition: all 1s;
}
.list-leave-active{
  position: absolute;
  width: calc(76% - 10px);
}
</style>
