<template>
  <vista/>
  <HelloWorld />

</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import vista from '@/components/vista.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,vista
  }
}
</script>
