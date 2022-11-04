<template lang="html">

  <section class="src-componentes-navbar">
      <nav class="navbar navbar-expand-md navbar-dark bg-dark">

        <router-link to="/">
          <a class="navbar-brand" href="#">Inicio</a>
        </router-link>
        
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">

            <!-- navegación binding -->
            <li class="nav-item">
              <router-link to="/formulario">
                <a class="nav-link" href="#">Formulario</a>
              </router-link>
            </li>

            <!-- navegación estructura -->
            <li class="nav-item">
              <router-link to="/respuestas-choice">
                <a class="nav-link" href="#">Respuestas Choice</a>
              </router-link>
            </li>          
          </ul>
        </div>
      </nav>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-components-nav-bar',
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  
</style>
