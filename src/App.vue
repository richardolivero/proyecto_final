<template>

 <!--  <nav class="navbar navbar-dark navbar-expand-lg bg-dark ">
    <div class="container-fluid">
      <h1 class="navbar-brand text-white">PROYECTO FINAL CRUD</h1>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon "></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-link" aria-current="page" @click="home">Mostrar Datos</a>|
          <a class="nav-link" @click="about">AgregarDatos</a>

        </div>
      </div>
    </div>
  </nav> -->



  <router-view />
</template>
<script>
export default {
  name: 'app',
  methods: {
    home() {
      this.$router.push('/home')
    },
    about() {

      this.$router.push({
        name: 'about',
        params: { Id: 0 }
      })

    }
  }
}
</script>

<style>
#app {
  font-family:'Times New Roman', Times, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;


}

.nav-link {
  cursor: pointer;
}
</style>
<!-- <form class="container-fluid justify-content-center">
  <button class="btn btn-outline-success me-2" type="button" @click="home">Mostrar Datos</button>
  <button class="btn btn-outline-success me-2" type="button" @click="about">Agregar Datos</button>
</form> -->