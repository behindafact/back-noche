<template>
  <div class="home">
    <the-home />
  </div>
</template>

<script>
// @ is an alias to /src
import TheHome from '@/components/TheHome.vue'

export default {
  //acá normalmente va el nombre del view
  name: 'Home',
  components: {
    TheHome
  }
}
</script>
