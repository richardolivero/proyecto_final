<template>

 <nav class="navbar navbar-dark navbar-expand-lg bg-dark ">
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
  </nav>
</template>

<script>
export default {
  name: 'vista',
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