<template>
  <div>
    <div class="home">
      <Home></Home>
    </div>
  </div>

</template>

<script>
// @ is an alias to /src
import Home from '@/components/Home.vue'


export default {
  name: 'Form',
  components: {
    Home
  },
  methods: {
    userExist: function () {
      let candidato = "";
      if (this.$isMobile()) {
        candidato = JSON.parse(localStorage.getItem('candidatoLocal'));
      } else {
        candidato = JSON.parse(this.$cookie.get("test"))
      }
      console.log("data", candidato);
      if (candidato === null) {
        return false;
      }
      return true;

    }
  }
}
</script>
