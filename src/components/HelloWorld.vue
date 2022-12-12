<template>
  <h1 v-if="(lista_estudiantes.length == 0)">no hay elementos</h1>
  <nav class="navbar bg-light">
    <div class="container-fluid">
      <form class="d-flex" role="search">
        <input class="form-control me-2" type="search" v-on:keyup="filtro_Id" placeholder="busque por Id" aria-label="Search" v-model="busqueda" v-if="(lista_estudiantes.length > 10)">
        <input class="form-control me-2" type="search" v-on:keyup="filtro_Apellido" placeholder="busque por Apellido" aria-label="Search" v-model="Apellido" v-if="(lista_estudiantes.length > 10)">
        
      </form>
    </div>
  </nav>

  <div class="container mt-4 ">
    <table class="table card-body " v-if="(lista_estudiantes.length > 0)">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">nombre</th>
          <th scope="col">apellido</th>
          <th scope="col">telefono</th>
          <th scope="col">ciudad</th>
          <th scope="col">carrera</th>
          <th scope="col">ACCIONES</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="elemento in lista_estudiantes" :key="elemento.Id_estudiante">
          <th scope="row">{{ elemento.Id_estudiante }}</th>
          <td class="col">{{ elemento.Nombre }}</td>
          <td class="col">{{ elemento.Apellido }}</td>
          <td class="col">{{ elemento.Telefono }}</td>
          <td class="col">{{ elemento.Ciudad }}</td>
          <td class="col">{{ elemento.Carrera }}</td>
          <td class="col">
            <span class="cursor badge text-bg-warning" title="editar"><i class=" bi bi-pen-fill text-light"
                @click="editar(elemento.Id_estudiante)"></i></span>
            |
            <span class="cursor badge text-bg-danger"  title="eliminar"><i class="bi bi-file-earmark-x"
                @click="borrar(elemento.Id_estudiante)"></i></span>
          </td>
        </tr>
      </tbody>
    </table>
  
  </div>

</template>

<script>

import axios from "axios";
export default {
  name: 'HelloWorld',
  data() {
    return {
      lista_estudiantes: [],
      estudiante_seleccionado: "",
      busqueda: '',
      Apellido:'',
    }
  },
  mounted() {

    this.listar_estudiantes();

  },
  methods: {
    borrar(Id) {

      axios.delete('http://localhost/matricula_API/estudiante/' + Id).then((response) => {
        alert('usuario eliminado')
        this.listar_estudiantes()
      }).catch((error) => {
        console.log(error)
      })
      //console.log(Id_estudiante)
      // axios.delete('http://localhost/matricula_API/estudiante/Id_estudiante')

    },
    editar(Id) {
      this.$router.push({
        name: 'about',
        params: { Id: Id }
      })
      console.log('click' + Id)
    },
    listar_estudiantes() {
      axios.get('http://localhost/matricula_API/estudiante').then((response) => {
        this.lista_estudiantes = response['data'];
      })
        .catch((error) => {
          console.log(error)
        })
    },
    filtro_Id(event) {
      event.preventDefault();

      console.log(this.lista_estudiantes);

      if (this.busqueda != '') {
        let result = this.lista_estudiantes.filter(item => item.Id_estudiante == this.busqueda)
        if (result.length > 0) {
          this.lista_estudiantes = result
        } 
        else {
          this.listar_estudiantes()
        }
      }
      else {
        this.listar_estudiantes()
        
      }
    },
    filtro_Apellido(event) {
      event.preventDefault();

      console.log(this.lista_estudiantes);

      if (this.Apellido != '') {
        let result = this.lista_estudiantes.filter(item => item.Apellido.toLowerCase().toString().startsWith(this.Apellido.toLowerCase().toString()))
        if (result.length > 0) {
          this.lista_estudiantes = result
        } 
        else {
          this.listar_estudiantes()
        }
      }
      else {
        this.listar_estudiantes()
        
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
