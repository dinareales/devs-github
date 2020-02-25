<template>
  <div class="home">
    <b-container>
      <b-row>
        <b-col>
          <div class="card-img-left">
            <img alt="Vue logo" src="../assets/logo.png">
            <p>Evaluador de candidatos con github</p>
          </div>
        </b-col>
        <b-col>
          <b-card class="mt-3" header="Información del candidato">
            <FormUser></FormUser>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import FormUser from '@/components/Form.vue'

export default {
  name: 'Form',
  components: {
    FormUser
  }
}
</script>
<style scoped>

  .card-img-left{
    text-align: center;
    padding: 0 auto;
    margin: 30%;
  }
  img{
    max-width: 250px;
  }
  p{
    padding-top: 5%;
    font-weight: bold;

  }
</style>
