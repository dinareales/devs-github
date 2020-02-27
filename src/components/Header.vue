<template>
    <div>
        <b-container class="container-bg">
            <div class="test-list row">
                <div sm="auto" cols="3" align="center" class="col-sm-2"><img class="img-center" :src=info.avatar_url></div>
                <div cols="9" class="col-sm-10">
                    <p>{{ candidato["name"]}} (Git:{{info.login}}) </p>
                    <p><span>Bio: </span> {{info.bio}}</p>
                </div>
            </div>
            <div class="row">
                <div class="col-sm">
                    <p><span>Cedula: </span>{{ candidato["cedula"]}}</p>
                </div>
                <div class="col-sm">
                    <p><span>Fecha de Nacimiento: </span>{{ candidato["fechaNacido"]}}</p>
                </div>
                <div class="col-sm">
                    <p><span>Email: </span>{{ candidato["email"]}}</p>
                </div>
            </div>
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
            //console.log("data", this.candidato["usuario"]);
        },
        mounted() {
            axios.get("https://api.github.com/users/"+this.candidato["usuario"])
                .then(response => this.info = response.data)
                .catch(err => {
                    console.log("Fallo")
                    // Manage the state of the application if the request
                    // has failed
                })
        }
    }
</script>
<style scoped>
    .img-center{
        max-height: 100px;
        border-radius: 50%;
        margin-top: 10px;
        text-align: center;
    }
    .container-bg{
        background: #e9ecef;
    }
    span{
        color: #dc3545;
    }
    p{
        padding: 10px;
        margin: auto;
    }

</style>
