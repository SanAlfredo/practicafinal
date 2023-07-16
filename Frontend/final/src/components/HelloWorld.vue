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
    <slot name="malla"></slot>
    
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      tamanio: "large"
    }
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
