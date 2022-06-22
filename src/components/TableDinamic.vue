<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-6 col-xs-12">
          <h1>Agregar notas</h1>
          <label>Nombre</label>
          <input type="text" class="form-control" v-model="nombre">
          <label>Nota</label>
          <input type="number" class="form-control" min="1" step="1" v-model="promedio" max="100">
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
              <tbody id="table-body">

              </tbody>
            </table>
          </div>
        </div>

      </div>

    </div>
    <div id="total">
    </div>

    <h5 class="mt-3">Porcentaje de estudiantes malos</h5>
    <div class="progress m-auto  col-8">
      <div id="progress-malos"
           class="progress-bar"
           role="progressbar"
           aria-valuenow="25"
           aria-valuemin="0"
           aria-valuemax="100"
      >
      </div>
    </div>
    <h5 class="mt-3">Porcentaje de estudiantes regulares</h5>
    <div class="progress m-auto  col-8">
      <div id="progress-regular"
           class="progress-bar"
           role="progressbar"
           aria-valuenow="25"
           aria-valuemin="0"
           aria-valuemax="100"
      >
      </div>
    </div>
    <h5 class="mt-3">Porcentaje de estudiantes buenos</h5>
    <div class="progress m-auto mb-5 col-8">
      <div id="progress-buenos"
           class="progress-bar"
           role="progressbar"
           aria-valuenow="25"
           aria-valuemin="0"
           aria-valuemax="100"
      >
      </div>
    </div>
  </div>
</template>

<script>


class Subject {
  constructor() {
    this.observers = [];
  }

  //Se agrega observadores.
  susbcribe(obs) {
    this.observers.push(obs);
  }

  //Se elimina observadores.
  unsubscribe(obs) {
    this.observers = this.observers.filter((el) => el != obs);
  }

  //Cambios de estado se notifica.
  notify(objeto) {
    this.observers.forEach((obs) => {
      obs.notify(objeto);
    });
  }
}

//Herencia
// eslint-disable-next-line no-unused-vars
class ItemSubject extends Subject {

  constructor() {
    super();
    this.items = [];
  }

  notify(item) {
    console.log(item)
    this.items.push(item);

    super.notify(this);
  }
}

// eslint-disable-next-line no-unused-vars
class ListObserver {
  constructor(tag) {
    this.tag = tag;
  }

  notify(subject) {
    // this.tag.innerHTML = "";
    console.log(this.tag)
    console.log(subject.items)

    subject.items.forEach(e => {
      console.log(e)
      this.tag.innerHTML = ''
      for (let index = 0; index < subject.items.length; index++) {
        if (parseFloat(subject.items[index].promedio) <= 25.0) {
          this.tag.innerHTML += '<tr><th>' + subject.items[index].nombre + '</th><th style="color:red; background: #3f3f3f">' + subject.items[index].promedio + '</th></tr>';
        }
        if (parseFloat(subject.items[index].promedio) > 25.0 && parseFloat(subject.items[index].promedio) <= 75.0) {
          this.tag.innerHTML += '<tr><th>' + subject.items[index].nombre + '</th><th style="color:yellow; background: #3f3f3f">' + subject.items[index].promedio + '</th></tr>';
        }
        if (parseFloat(subject.items[index].promedio) > 75.0 && parseFloat(subject.items[index].promedio) <= 100.0) {
          this.tag.innerHTML += '<tr><th>' + subject.items[index].nombre + '</th><th style="color:green; background: #3f3f3f">' + subject.items[index].promedio + '</th></tr>';
        }
        // this.tag.innerHTML += '<tr><th>'+subject.items[index].nombre +'</th><th>'+subject.items[index].promedio+'</th></tr>' ;
      }
    })
  }
}

// eslint-disable-next-line no-unused-vars
class TotalObserverBad {
  constructor(tag) {
    this.tag = tag;
  }

  notify(subject) {

    subject.items.forEach(e => {
      console.log(e)
      this.tag.innerHTML = ''
      let aux = 0;
      for (let index = 0; index < subject.items.length; index++) {
        console.log(aux);
        if (parseFloat(subject.items[index].promedio) <= 25.0) {
          // eslint-disable-next-line no-unused-vars
          aux++;
        }
      }
      console.log(aux / subject.items.length);
      this.tag.innerHTML = ((aux / subject.items.length) * 100).toFixed(2) + '%';
      this.tag.style.cssText = 'width:' + (aux / subject.items.length) * 100 + '%; background:red; color:black; font-weight:bolder';

    })
  }
}

class TotalObserverRegular {
  constructor(tag) {
    this.tag = tag;
  }

  notify(subject) {

    subject.items.forEach(e => {
      console.log(e)
      this.tag.innerHTML = ''
      let aux = 0;
      for (let index = 0; index < subject.items.length; index++) {
        console.log(aux);
        if (parseFloat(subject.items[index].promedio) > 25.0 && parseFloat(subject.items[index].promedio) <= 75.0) {
          // eslint-disable-next-line no-unused-vars
          aux++;
        }
      }
      console.log(aux / subject.items.length);
      this.tag.innerHTML = ((aux / subject.items.length) * 100).toFixed(2) + '%';
      this.tag.style.cssText = 'width:' + (aux / subject.items.length) * 100 + '%;background:yellow; color:black; font-weight:bolder';

    })
  }
}

// eslint-disable-next-line no-unused-vars
class TotalObserverGood {
  constructor(tag) {
    this.tag = tag;
  }

  notify(subject) {

    subject.items.forEach(e => {
      console.log(e)
      this.tag.innerHTML = ''
      let aux = 0;
      for (let index = 0; index < subject.items.length; index++) {
        console.log(aux);
        if (parseFloat(subject.items[index].promedio) > 75.0 && parseFloat(subject.items[index].promedio) <= 100.0) {
          // eslint-disable-next-line no-unused-vars
          aux++;
        }
      }
      console.log(aux / subject.items.length);
      this.tag.innerHTML = ((aux / subject.items.length) * 100).toFixed(2) + '%';
      this.tag.style.cssText = 'width:' + (aux / subject.items.length) * 100 + '%; background:green; color:black; font-weight:bolder';

    })
  }
}

let itemsSubject = new ItemSubject();

export default {
  name: "TableDynamic",
  el: '#app',
  data() {
    return {
      lista: {},
      nombre: '',
      promedio: '',
    }
  },
  methods: {
    agregarnota: function () {
      let listObserver = new ListObserver(document.getElementById("table-body"));
      let totalObserver = new TotalObserverBad(
          document.getElementById("progress-malos")
      );
      let totalObserver1 = new TotalObserverRegular(
          document.getElementById("progress-regular")
      );
      let totalObserver2 = new TotalObserverGood(
          document.getElementById("progress-buenos")
      );
      itemsSubject.susbcribe(listObserver);
      itemsSubject.susbcribe(totalObserver);
      itemsSubject.susbcribe(totalObserver1);
      itemsSubject.susbcribe(totalObserver2);
      itemsSubject.unsubscribe(totalObserver1)
      if (parseInt(this.promedio) > 100) {
        alert("El promedio no debe ser mayor a 100")
      } else {
        if (this.nombre != "" && this.promedio != "" && parseInt(this.promedio) <= 100) {
          // this.lista.push({nombre: this.nombre, promedio: this.promedio});
          console.log(this.promedio)
          console.log(this.nombre)
          itemsSubject.notify({
            nombre: this.nombre,
            promedio: this.promedio,
          });
        } else {
          alert("ingrese el nombre y la nota del estudiante")
        }
      }
    },
  }
  , computed: {
  }
}
</script>
<style scoped>
#table {
  max-height: 250px;
}
</style>