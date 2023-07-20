<template>
  <div class="about">
    <div class="img-conteiner" align="center">
      <img :src="logo" alt="" width="800" />
    </div>
    <h1 class="textos">Física FCPN - UMSA</h1>
    <p class="listas"><i>Carrera de Física dependiente de la Facultad de Ciencias Puras y Naturales de la UMSA, se
        encuentra situada en Cota - Cota calle 27, donde se cuenta con laboratorios:</i></p>
    <ul>
      <li class="listas">Física de partículas</li>
      <li class="listas">Física de atmósfera</li>
      <li class="listas">Física del estado sólido</li>
    </ul>
    <div class="row" v-for="(item, key) in acerca">
      <h3 class="textos" style="text-transform: uppercase;">{{ key }}</h3>
      <p class="listas"><i>{{ item }}</i> </p>
    </div>
  </div>
  <FooterApp></FooterApp>
</template>
<style type="text/css">
.textos {
  text-align: center;
  color: midnightblue
}

.listas {
  text-align: center;
  color: darkgreen;
  font-size: large;
}
</style>
<script>
import FooterApp from '@/components/Footer.vue'
export default {
  name: 'AboutView',
  data() {
    return {
      logo: "https://blog.advesa.com/wp-content/uploads/2019/11/about-us-page.png",
      acerca:
      {
        objetivo: "Formar nuevos profesionales en el área científica de la física, para enriquecer la comunidad científica de Bolivia y ser competitivos a nivel mundial.",
        mision: "Brindar una educación de calidad, con docentes especializados, para dotar al estudiante de las armas necesarias para afrontar los problemas que se le presenten en la vida cotidiana.",
        vision: "Los estudiantes que se forman en la Universidad debe ser los principales promotores de la ciencia en nuestro País."
      }
    }
  },
  components: {
    FooterApp
  }
}
</script>