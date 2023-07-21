<template>
  <div class="about">
    <center>
      <h3>Listado y registro de estudiantes</h3>
    </center>

    <Tablas>
      <template v-slot:lista>

        <table class="highlight responsive-table ">
          <thead>
            <tr>
              <th>Nombre</th>
              <th>Nacimiento</th>
              <th>Carnet</th>
              <th>Foto</th>
              <th></th>
            </tr>
          </thead>

          <tbody style="width: fit-content;white-space: nowrap;">
            <tr v-for="item in estudiantes" style="padding: 0%;">
              <td>{{ item.nombre }}</td>
              <td>{{ item.nacimiento }}</td>
              <td>{{ item.carnet }}</td>
              <td>
                <figure>
                  <img :src="this.api + `/estudiantes/foto/${item.foto}`" style="width: 30%; height: 30%;">
                </figure>
              </td>
              <td>
                <router-link :to="'/editar/estudiante/' + item.id"><i class="material-icons">create</i></router-link>
                <i class="material-icons" style="color:red" @click="eliminarItem(item.id)">delete_forever</i>
              </td>
            </tr>
          </tbody>
        </table>
      </template>
      <template v-slot:nuevo>
        <div class="row card p-2" style="max-width: 650px;">
          <h6>Formulario de registro estudiante</h6>
          <form class="col s12" @submit.prevent="saveEstudent()">
            <div class="row">
              <div class="input-field col s12">
                <input id="nombre" type="text" class="validate" v-model="estudianteload.nombre">
                <label for="nombre"> Nombre completo</label>
              </div>
            </div>
            <div class="row">
              <div class="input-field col s12">
                <input id="nacimiento" type="date" class="validate" v-model="estudianteload.nacimiento">
                <label for="nacimiento"> Fecha de Nacimiento</label>
              </div>
            </div>
            <div class="row">
              <div class="input-field col s12">
                <input id="carnet" type="number" class="validate" v-model="estudianteload.carnet">
                <label for="carnet"> Carnet de Identidad</label>
              </div>
            </div>
            <div class="row">
              <div class="input-field col s12">
                <label for="foto"> Fotografia</label>
                <br><br>
                <input id="foto" type="file" class="validate" @change="obtenerImagen">
                <figure>
                  <img :src="imagen" style="width: 30%; height: 30%;">
                </figure>
              </div>
            </div>
            <div class="row">
              <div class="input-field col s12">
                <button class="btn waves-effect waves-light" type="submit" name="action">Submit
                  <i class="material-icons right">send</i>
                </button>
              </div>
            </div>
          </form>
        </div>
      </template>
    </Tablas>
  </div>
  <FooterApp></FooterApp>
</template>
<script>
// @ is an alias to /src
import FooterApp from '@/components/Footer.vue'
import Tablas from '@/components/Tablas.vue'


export default {
  name: 'RegistroView',
  components: {
    FooterApp, Tablas
  },
  data() {
    const api = process.env.VUE_APP_API
    return {
      api,
      imagenMiniatura: "",
      estudiantes: [],
      fichero: null,
      estudianteload: {
        nombre: "",
        nacimiento: "",
        carnet: null,
        foto: ""
      }
    }
  },
  methods: {
    getEstudiantes() {
      this.axios({
        method: "get",
        url: this.api + '/estudiantes'
      }).then((response) => {
        this.estudiantes = response.data;
        console.log(this.estudiantes);
      }).catch((error) => {
        console.log(error);
      }).finally(() => { })
    },
    saveEstudent() {
      if (this.estudianteload.nombre == "" || this.estudianteload.nacimiento == "" || this.estudianteload.carnet == null || this.fichero == null) {
        alert("Debe llenar todos los campos y seleccionar una foto");
      } else {
        const formdata = new FormData();
        formdata.append('file', this.fichero);
        this.axios({
          method: 'post',
          url: this.api + '/estudiantes/foto',
          data: formdata
        }).then((response) => {
          console.log(response.data[0].filename);
          this.estudianteload.foto = response.data[0].filename;
          this.saveEstudiante();
        }
        ).catch((error) => { console.log(error) });
      }
    },
    saveEstudiante() {
      this.axios({
        method: 'post',
        url: this.api + '/estudiantes',
        data: this.estudianteload
      })
        .then((response) => {
          this.estudianteload = {
            nombre: "",
            nacimiento: "",
            carnet: null,
            foto: "",
          };
          this.fichero = null;
          setTimeout(function () {
            var elems = document.querySelectorAll('select');
            var select = M.FormSelect.init(elems);
          });
          this.getEstudiantes();
          console.log(response);
        }).catch((error) => {
          console.log(error)
        });
    },
    obtenerImagen(e) {
      let file = e.target.files[0];
      const allowedTypes = ["image/jpg", "image/jpeg", "image/png", "image/gif"];
      if (allowedTypes.includes(file.type)) {
        this.fichero = file;
        this.cargarImagen(file);
      } else {
        alert("el tipo de archivo debe ser una imagen");
      }
    },
    cargarImagen(file) {
      let reader = new FileReader();
      reader.onload = (e) => {
        this.imagenMiniatura = e.target.result;
      }
      reader.readAsDataURL(file);
    }
  },
  computed: {
    imagen() {
      return this.imagenMiniatura;
    }
  },
  mounted() {
    this.getEstudiantes();
  },
  created() {
    setTimeout(() => {
      var elems = document.querySelectorAll('select');
      var select = M.FormSelect.init(elems);
    });
  }
}
</script>