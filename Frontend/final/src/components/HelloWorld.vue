<template>
  <div class="hello">
    <center>
      <h1><i>{{ msg }}</i></h1>
      <br>
    </center>
    <p :style="{ fontSize: tamanio }">
      Web dedicada a los docentes de la carrera de Física en la faculta de Ciencias Puras y Naturales de la UMSA
      <a href="http://www.fiumsa.edu.bo/" target="_blank" rel="noopener"><i><u>visita nuestra página
            oficial</u></i></a>.
    </p>

    <center>
      <h3>Malla curricular</h3>
      <br>
      <img src="../assets/f7.jpg" style="width: 70%;">
      <h3>Materias por semestre</h3>
    </center>
    <p :style="{ fontSize: tamanio }">
      Presentamos las materias por semestre que lleva un alumno de la carrerra
    </p>
    <ul v-for="item in items">
      <h4>{{ item.semestres.nombre }}</h4>
      <li style="text-transform: uppercase;">{{ item.codigos.nombre }} - {{ item.cod }} {{ item.nombre }}</li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a>
      </li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    const api = process.env.VUE_APP_API
    return {
      api,
      tamanio: "large",
      items: []
    }
  },
  methods: {
    getMaterias() {
      this.axios({
        method: "get",
        url: this.api + '/materias?_expand=codigos&_expand=semestres'
      }).then((response) => {
        this.items = response.data;
        console.log(this.items);
      }).catch((error) => {
        console.log(error);
      }).finally(() => { })
    }
  },
  mounted(){
    this.getMaterias();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
