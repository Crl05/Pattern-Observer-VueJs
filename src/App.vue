<template>
  <div id="content-principal">
    <h1 class="fw-bolder" id="title">Patron Observador</h1>
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Js</h1>

  </div>
  <div id="present" class="mb-5 mt-4">
    <h5 class="fw-bold">Presentador por:</h5>
    <h5 class="fw-light">Carlos Amaya & Pablo Herrera</h5>
  </div>
  <div id="content-text" class="col-xl-8 m-auto">
    <h4>El patrón de diseño <a href="https://reactiveprogramming.io/blog/es/patrones-de-diseno/observer"
                               class="fw-bold">Observer</a> permite observar los cambios producidos por un objeto, de
      esta forma, cada cambio
      que afecte el estado del objeto observado lanzará una notificación a los observadores; a esto se le conoce como
      Publicador-Suscriptor. Observer es uno de los principales patrones de diseño utilizados en interfaces gráficas de
      usuario (GUI), ya que permite desacoplar al componente gráfico de la acción a realizar.</h4>
  </div>

  <img class="mt-4 mb-4 col-5 img-thumbnail" src="./assets/img.png" alt="representacion patron observer">
  <div id="content-text" class="mt-4 col-xl-8 m-auto">
    <h4>En conclusion: notificar a varios objetos sobre cualquier evento que le suceda al objeto que están
      observando.</h4>

  </div>
  <div class="col-8 m-auto mt-5">
    <hr class="mt-3 rounded" style="color: #2c3e50; height: 7px" />
    <h2 class="fw-bold">En Vue Js</h2>
    <h4 class="fw-light text-justify mt-4">Una de las características más distintivas de Vue es el sistema de
      reactividad discreto. El estado de los componentes son objetos JavaScript reactivos. Cuando los modifica, la vista
      se actualiza. Hace que la administración del estado sea simple e intuitiva, pero también es importante comprender
      cómo funciona para evitar algunos errores comunes. En esta sección, profundizaremos en algunos de los detalles de
      nivel inferior del sistema de reactividad de Vue.</h4>
    <h3 class="fw-bold mt-5">Comuted</h3>
    <h4 class="fw-light ext-justify mt-4">hay varias maneras de establecer valores estáticos o dinámicos para mostrar en
      la plantilla. Estas incluyen el uso de la interpolación de texto, la codificación directa en su HTML, o incluso el
      uso de expresiones simples para modificar los datos.</h4>
    <h4>Aquí es donde las propiedades computadas son muyd útiles. En este tutorial, repasaremos los fundamentos del uso
      de las propiedades computadas en Vue.js. A continuación, pondremos en práctica todas nuestras nuevas habilidades
      construyendo una aplicación de ejemplo en vivo.</h4>
    <h3 class="fw-bold mt-5">Aplicacion</h3>


  </div>
  <TableDynamic class="border border-5 col-10 m-auto mt-5 shadow shadow-3 mb-5 p-2"></TableDynamic>
</template>

<script>
import TableDynamic from './components/TableDinamic.vue'

export default {
  name: 'App',
  components: {
    TableDynamic,
  }
}
</script>

<style>
#present, h5 {
  line-height: 0px;
  font-weight: lighter;
}

h1, #title {
  margin-right: 15px;
}

#content-text {
  display: grid;
  justify-items: center;
  align-items: center;
}

h4 {
  text-align: justify;
}

#content-principal {
  display: flex;
  justify-items: center;
  align-items: center;
  justify-content: center;
}

img {
  height: 55px;
  width: 55px;

}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
