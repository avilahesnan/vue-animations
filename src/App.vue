<template>
  <div id="app">

    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <p class="lead">Treinando transição/animação de elementos/components no Vue.</p>
      </div>
    </div>

    <div class="container">
      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>

      <div class="form-group">
        <label>Animações</label>
        <select class="form-control" v-model="animacaoSelecionada">
          <option value="fade">Fade</option>
          <option value="zoom">Zoom</option>
          <option value="slide">Slide</option>
        </select>
      </div>

      <div class="form-group">
        <label>Mensagens</label>
        <select class="form-control" v-model="alertaAtual">
          <option value="info">Info</option>
          <option value="warning">Warning</option>
          <option value="success">Success</option>
        </select>
      </div>

      <div class="form-group">
        <label>Components</label>
        <select class="form-control" v-model="componentSelecionado">
          <option value="AppHome">Home</option>
          <option value="AppSobre">Sobre</option>
        </select>
      </div>
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
        <div class="alert alert-primary" v-if="mostrar">Animações no VueJS</div>
      </transition> -->

      <!-- <transition 
      appear
      appear-class=""
      appear-active-class="animate__animated animate__flipInY"
      appear-to-class=""
      @before-appear="beforeAppear"
      @appear="appear"
      @after-appear="afterAppear"
      @appear-cancelled="appearCancelled"
      enter-class=""
      enter-active-class="animate__animated animate__bounceInLeft"
      enter-to-class=""
      leave-class=""
      leave-active-class="animate__animated animate__bounceOutDown"
      leave-to-class=""
      >
        <div class="alert alert-primary" v-if="mostrar">Animações no VueJS</div>
      </transition> -->

      <transition :name="animacaoSelecionada" mode="out-in">
        <!-- <div :class="classesAlerta" :key="alertaAtual">Animações no VueJS</div> -->
        <component :is="componentSelecionado"></component>
      </transition>
    </div>

  </div>
</template>

<script>

export default {
  components: {
    AppHome: () => import('./components/AppHome.vue'),
    AppSobre: () => import('./components/AppSobre.vue')
  },
  data () {
    return {
      mostrar: true,
      animacaoSelecionada: 'fade',
      alertaAtual: 'info',
      componentSelecionado: 'AppHome'
    }
  },
  computed: {
    classesAlerta () {
      return {
        alert: true,
        [`alert-${this.alertaAtual}`]: true
      }
    }
  },
  methods: {
    beforeEnter (el) {
      console.log('beforeEnter')
      el.style.opacity = 0
    },
    enter () {
      console.log('enter')
    },
    afterEnter () {
      console.log('afterEnter')
    },
    enterCancelled () {
      console.log('enterCancelled')
    },
    beforeLeave (el) {
      console.log('beforeLeave')
      el.style.transtionn = 'width 0.1s'
      el.style.overflow = 'hidden'
      el.style.whitespace = 'nowrap'
    },
    leave () {
      console.log('leave')
    },
    afterLeave () {
      console.log('afterLeave')
    },
    leaveCancelled () {
      console.log('leaveCancelled')
    },
    beforeAppear () {
      console.log('beforeAppear')
    },
    appear () {
      console.log('appear')
    },
    afterAppear () {
      console.log('afterAppear')
    },
    appearCancelled () {
      console.log('appearCancelled')
    },
  }
}
</script>

<style>
  body {
    overflow: hidden;
  }
</style>

<style scoped>
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }

  .zoom-enter, .zoom-leave-to {
    transform: scale(0);
  }

  .zoom-enter-active, .zoom-leave-active {
    transition: transform 0.5s;
  }

  .slide-enter, .slide-leave-to {
    opacity: 0;
  }

  .slide-enter-active {
    animation: slide-transition 0.7s;
    transition: opacity 0.7s;
  }

  .slide-leave-active {
    animation: slide-transition 0.7s reverse;
    transition: opacity 0.7s;
  }

  @keyframes slide-transition {
    0% {
      transform: translateX(-100px);
    }

    100% {
      transform: translateX(0px);
    }
  }
</style>