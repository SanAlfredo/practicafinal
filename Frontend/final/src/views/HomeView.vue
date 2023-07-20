<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/registro.png" style="width: 100%;">
    <HelloWorld msg="Bienvenidos a Física - FCNP - UMSA">
      <template v-slot:malla>
        <div v-for="item in semestres">
          <h4>{{ item.nombre }}</h4>
          <ul v-for="items in materias">
            <li style="text-transform: uppercase;" v-if="item.nombre === items.semestre.nombre">{{ items.codigo.nombre
            }} - {{ items.cod }} {{ items.nombre }}</li>
          </ul>
        </div>
        
      </template>
    </HelloWorld>
  </div>
  <FooterApp></FooterApp>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import FooterApp from '@/components/Footer.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    FooterApp
  },
  data() {
    const api = process.env.VUE_APP_API
    return {
      api,
      materias: [],
      semestres: []
    }
  },
  methods: {
    getMaterias() {
      this.axios({
        method: "get",
        url: this.api + '/materias/todo'
      }).then((response) => {
        this.materias = response.data;
        console.log(this.items);
      }).catch((error) => {
        console.log(error);
      }).finally(() => { })
    },
    getSemestres() {
      this.axios({
        method: "get",
        url: this.api + '/semestres'
      }).then((response) => {
        this.semestres = response.data;
        console.log(this.items);
      }).catch((error) => {
        console.log(error);
      }).finally(() => { })
    }
  },
  mounted() {
    this.getMaterias();
    this.getSemestres();
  }
}
</script>
