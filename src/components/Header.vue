<template>
    <div>
        <b-container class="bv-example-row ">
            <b-row class="test-list">
                <b-col cols="4" class="bg-secondary text-white">Imagen de perfil GITHUB</b-col>
                <b-col cols="8" class="bg-success text-white">
                    <p>{{ candidato["name"]}} (Git:{{info}}) </p>
                    <p>Bio: </p>
                </b-col>
            </b-row>
            <b-row>
                <b-col class= "bg-primary text-white">
                    <p>Cedula: {{ candidato["cedula"]}}</p>
                </b-col>
                <b-col class= "bg-primary text-white">
                <p>Fecha de Nacimiento: {{ candidato["fechaNacido"]}}</p>
            </b-col>
                <b-col class= "bg-primary text-white">
                    <p>Email: {{ candidato["email"]}}</p>
                </b-col>
            </b-row>
        </b-container>
    </div>
</template>
<script>
    import axios from "axios";

    export default {
        name: "UserHeader",
        data() {
            return {
                candidato: {},
                info: []
            }
        },
        created: function () {
            if (this.$isMobile()) {
                this.candidato = JSON.parse(localStorage.getItem('candidatoLocal'));
            } else {
                this.candidato = JSON.parse(this.$cookie.get("candidatoLocalPC"))
            }
            console.log("data", this.candidato["usuario"]);
        },
        mounted() {
            axios.get("https://api.github.com/users/dinareales")
                .then(response => this.info = response.data.login )
                .catch(err => {
                    console.log("Fallo")
                    // Manage the state of the application if the request
                    // has failed
                })
        }
    }
</script>
