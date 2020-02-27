<template>
    <div>
        <b-form @submit="onSubmit" v-if="show" class="container">
            <b-card class="mt-3" header="Información del candidato">
                <b-form-group id="input-group-1" label="Nombre y apellido: " label-for="input-1">
                    <b-form-input
                            id="input-1"
                            v-model="form.name"
                            placeholder="Ingrese su nombre completo"
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-2" label="Cédula: " label-for="input-2">
                    <b-form-input
                            id="input-2"
                            v-model="form.cedula"
                            type="number"
                            placeholder="Ingrese su cédula de ciudadanía"
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-3" label="Fecha de Nacimiento: " label-for="input-3">
                    <b-form-input
                            id="input-3"
                            v-model="form.fechaNacido"
                            type="date"
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-4" label="Email:" label-for="input-4">
                    <b-form-input
                            id="input-4"
                            v-model="form.email"
                            type="email"
                            placeholder="Ingrese su email"
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-5" label="*Usuario de Github: " label-for="input-5">
                    <b-form-input
                            id="input-5"
                            v-model="form.usuario"
                            required
                            placeholder="Ingrese su usuario de github"
                    ></b-form-input>
                </b-form-group>

                <b-button type="submit" variant="primary">Consultar</b-button>
            </b-card>
        </b-form>
        <div  v-if="!show">
            <b-button v-on:click="exit" variant="danger">SALIR</b-button>
            <UserDetails></UserDetails>
        </div>
    </div>
</template>

<script>
    import UserDetails from '@/components/UserDetails.vue'
    export default {
        name: 'Home',
        components: {
            UserDetails
        },
        data() {
            return {
                form: {
                    name: '',
                    cedula: '',
                    fechaNacido: '',
                    email: '',
                    usuario: ''
                },
                show: true
            }
        },
        methods: {
            onSubmit(evt) {
                evt.preventDefault();
                let candidato =  JSON.stringify(this.form);
                if (this.$isMobile()) {
                    localStorage.setItem('candidatoLocal',candidato);
                } else {
                    this.$cookie.set('candidatoLocalPC', candidato, 1);
                }
                this.show = false;
            },
            exit: function () {
                if (this.$isMobile()) {
                    localStorage.removeItem('candidatoLocal');
                } else {
                    this.$cookie.delete("candidatoLocalPC");
                }
                this.show = true;
            }
        },
        created: function () {
                if (this.$isMobile()) {
                    this.candidato = JSON.parse(localStorage.getItem('candidatoLocal'));
                } else {
                    this.candidato = JSON.parse(this.$cookie.get("candidatoLocalPC"))
                }

                if(this.candidato !== null){ // esta logueado
                    this.show = false;
                }
        },
    }
</script>
<style scoped>
    .container{
        max-width: 700px;
    }
</style>
