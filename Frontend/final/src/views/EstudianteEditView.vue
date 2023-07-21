<template>
    <div>
        <h5>Editar un estudiante {{ $route.params.id }}</h5>
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
                        <div v-if="active === 1">
                            <img :src="this.api + `/estudiantes/foto/${estudianteload.foto}`"
                                style="width: 30%; height: 30%;">
                        </div>
                        <div v-if="active === 0">
                            <img :src="imagen" style="width: 30%; height: 30%;">
                        </div>
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
    name: 'EstudianteEdit',
    data() {
        const api = process.env.VUE_APP_API
        return {
            api,
            active: 1,
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
    components: {
        FooterApp
    },
    methods: {
        getEstudiante() {
            const id = this.$route.params.id;
            console.log("buscando el id: " + id);
            this.axios({
                method: 'get',
                url: this.api + '/estudiantes/' + id
            }).then((response) => {
                this.estudianteload = response.data;
                setTimeout(function () {
                    M.updateTextFields();
                });
                console.log(response);
            })
                .catch((error) => { console.log(error) })
                .finally(() => { });
        },
        saveEstudent() {
            if (this.estudianteload.nombre == "" || this.estudianteload.nacimiento == "" || this.estudianteload.carnet == null) {
                alert("Debe llenar todos los campos");
            } else {
                if (this.fichero == null) {
                    this.saveEstudiante();
                } else {
                    this.axios({
                        method: 'delete',
                        url: this.api + '/estudiantes/foto/' + this.estudianteload.foto
                    }).then((response) => {
                        if (response.data.message == "borrado exitoso") {
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
                        } else {
                            alert("ocurrio un problema para guardar la imagen");
                        }
                    }).catch((error) => {
                        console.log(error);
                    })
                }
            }
        },
        saveEstudiante() {
            this.axios({
                method: 'patch',
                url: this.api + '/estudiantes/' + this.$route.params.id,
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
                    console.log(response);
                }).catch((error) => {
                    console.log(error)
                }).finally(() => { });
        },
        obtenerImagen(e) {
            let file = e.target.files[0];
            this.active = false;
            const allowedTypes = ["image/jpg", "image/jpeg", "image/png", "image/gif"];
            if (allowedTypes.includes(file.type)) {
                this.fichero = file;
                this.active = 0;
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
    }, created() {
        this.getEstudiante();
    },
    computed: {
        imagen() {
            return this.imagenMiniatura;
        }
    },
}
</script>