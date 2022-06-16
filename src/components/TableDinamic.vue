<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-6 col-xs-12">
          <h1>Agregar notas</h1>
          <label>Nombre</label>
          <input type="text" class="form-control" v-model="nombre">
          <label>Nota</label>
          <input type="number" class="form-control" v-model="promedio" max="100">
          <input type="button" value="guardar" class="btn btn-success mt-3" v-on:click="agregarnota">
        </div>
        <div class="col-md-6 col-xs-12 ">
          <h1>Listado de notas</h1>
          <div id="table" class="overflow-auto">
            <table class="table table-striped table-hover">
              <thead>
              <tr>
                <th>Nombre</th>
                <th>Nota</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="(item,index) in lista" :key="index.id">
                <th v-text="item.nombre" class="fw-light"></th>
                <th v-text="item.promedio" class="fw-light"></th>
              </tr>
              </tbody>
            </table>
          </div>
        </div>

      </div>

    </div>
    <h5 class="mt-3">Porcentaje de estudiantes malos</h5>
    <div class="progress m-auto  col-8">
      <div
          class="progress-bar"
          role="progressbar"
          :style="{'width': calculemalos+'%'}"
          aria-valuenow="25"
          aria-valuemin="0"
          aria-valuemax="100"
          :class="colorm"

      >
        {{ calculemalos }}%
      </div>
    </div>
    <h5 class="mt-3">Porcentaje de estudiantes regulares</h5>
    <div class="progress m-auto  col-8">
      <div
          class="progress-bar"
          role="progressbar"
          :style="{'width': calculeregular+'%'}"
          aria-valuenow="25"
          aria-valuemin="0"
          aria-valuemax="100"
          :class="colorr"
      >
        {{ calculeregular }}%
      </div>
    </div>
    <h5 class="mt-3">Porcentaje de estudiantes buenos</h5>
    <div class="progress m-auto mb-5 col-8">
      <div
          class="progress-bar"
          role="progressbar"
          :style="{'width': calculebuenos+'%'}"
          aria-valuenow="25"
          aria-valuemin="0"
          aria-valuemax="100"
          :class="colorb"

      >
        {{ calculebuenos }}%
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TableDynamic",
  el: '#app',
  data() {
    return {
      lista: [],
      nombre: '',
      promedio: '',
    }
  },
  methods: {
    agregarnota: function () {
      if (this.nombre != "" && this.promedio != "") {
        this.lista.push({nombre: this.nombre, promedio: this.promedio});
        this.nombre = "";
        this.promedio = "";
      } else {
        alert("ingrese el nombre y la nota del estudiante")
      }
    }
  }
  , computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    calculemalos: function () {
      let M = 0;
      for (let i = 0; i < this.lista.length; i++) {
        if (parseInt(this.lista.at(i).promedio) <= 25) {
          // eslint-disable-next-line no-unused-vars
          M++;
        }
      }
      var total;
      if (M / this.lista.length) {
        total = (M / this.lista.length) * 100
      } else {
        total = 0;
      }
      return total;
    },
    calculeregular: function () {
      let M = 0;
      for (let i = 0; i < this.lista.length; i++) {
        if (parseInt(this.lista.at(i).promedio) > 25 && parseInt(this.lista.at(i).promedio) <=75) {
          // eslint-disable-next-line no-unused-vars
          M++;
        }
      }
      var total;
      if (M / this.lista.length) {
        total = (M / this.lista.length) * 100
      } else {
        total =
            0;
      }
      return total;
    },
    calculebuenos: function () {
      let M = 0;
      for (let i = 0; i < this.lista.length; i++) {
        if (parseInt(this.lista.at(i).promedio) > 75 && parseInt(this.lista.at(i).promedio) <=100) {
          // eslint-disable-next-line no-unused-vars
          M++;
        }
      }
      var total;
      if (M / this.lista.length) {
        total = (M / this.lista.length) * 100
      } else {
        total =
            0;
      }
      return total;
    },
    colorb: function () {
      return {
        'bg-danger': parseInt(this.calculebuenos) <= 25 ,
        'bg-warning': parseInt(this.calculebuenos)> 25 && parseInt(this.calculebuenos)<= 75,
        'bg-success': parseInt(this.calculebuenos)> 75 && parseInt(this.calculebuenos)<= 100,
      }
    },
    colorm: function () {
      return {
        'bg-danger': parseInt(this.calculemalos) <= 25 ,
        'bg-warning': parseInt(this.calculemalos)> 25 && parseInt(this.calculemalos)<= 75,
        'bg-success': parseInt(this.calculemalos)> 75 && parseInt(this.calculemalos)<= 100,
      }
    },
    colorr: function () {
      return {
        'bg-danger': parseInt(this.calculeregular) <= 25 ,
        'bg-warning': parseInt(this.calculeregular)> 25 && parseInt(this.calculeregular)<= 75,
        'bg-success': parseInt(this.calculeregular)> 75 && parseInt(this.calculeregular)<= 100,
      }
    },
  }

}
</script>
<style scoped>
#table {
  max-height: 250px;
}
</style>