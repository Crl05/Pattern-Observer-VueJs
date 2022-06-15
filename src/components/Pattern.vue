<script setup>
const theme = {
  color: 'blue',
  mayus: 'italic'
}
</script>
<template>
  <div id="app" class="container">
    <h3>{{ mensaje }}</h3>

    <button class="btn btn-primary" @click="contador++">+</button>
    <button class="btn btn-danger" @click="contador--">-</button>
    <h3>{{ contador }}</h3>
    <div class="progress">
      <div
          class="progress-bar"
          role="progressbar"
          :style="{'width': contador+'%'}"
          aria-valuenow="25"
          aria-valuemin="0"
          aria-valuemax="100"
          :class="color"
      >
        {{ contador }}%
      </div>
    </div>
  </div>
  <div id="computed_props">
    FirstName : <input type="text" v-model="firstname"/> <br/><br/>
    LastName : <input type="text" v-model="lastname"/> <br/><br/>
    <h1>My name is {{ firstname }} {{ lastname }}</h1>
    <h1>Using computed method : {{ getfullname }}</h1>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Pattern",
  el: ['#computed_props', '#app0'],
  data() {
    return {
      array: [
        {
          id: 1,
          nombre: "Pablo",
          numero: "12",
        },
        {
          id: 2,
          nombre: "Juan",
          numero: "15",
        },
        {
          id: 3,
          nombre: "Carlos",
          numero: "18",
        },
      ],
      mensaje: 'Pablo Herrera - Carlos Amaya',
      contador: 0,
      firstname: "",
      lastname: "",
      birthyear: "",

    }
  },
  computed: {
    color() {
      return {
        'bg-success': this.contador <= 25,
        'bg-warning': this.contador > 25 && this.contador <= 50,
        'bg-danger': this.contador > 50
      }
    }, etfullname: function () {
      return this.firstname + " " + this.lastname;
    }
  },

}
</script>

<style scoped>
#title {
  color: v-bind('theme.color');
  font-style: v-bind('theme.mayus');
}
</style>