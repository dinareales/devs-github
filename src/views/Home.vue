<template>
  <div class="home container">
    <FormUser> </FormUser>
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
