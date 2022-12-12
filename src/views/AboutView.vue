<template>

  <vista/>
  <AgregarDatos/>
</template>
<script>
// @ is an alias to /src
import AgregarDatos from '@/components/AgregarDatos.vue'
import vista from '@/components/vista.vue'
export default {
  name: 'About',
  components: {
    AgregarDatos,vista
  }
}
</script> 