<template>
  <div class="container  tt">
    <div class="card mt-3">
      <div class="card-body  text-black">
        <h5 class="card-title">Datos del estudiante</h5>
        <form>
          <div class="mb-3 form-group">
            <label for class="form-label ">Nombre</label>
            <input type="text" class="form-control" id="Nombre" aria-describedby="Nombre"
              placeholder="ingrese su nombre" v-model="Nombre">
          </div>
          <div class="mb-3">
            <label for="Apellido" class="form-label">Apellido</label>
            <input type="text" class="form-control" id="Apellido" aria-describedby="Apellido"
              placeholder="ingrese su apellido" v-model="Apellido">
          </div>
          <div class="mb-3">
            <label for="Telefono" class="form-label">Telefono</label>
            <input type="number" class="form-control" id="Telefono" aria-describedby="Telefono"
              placeholder="ingresa su numero de telefono" v-model="Telefono">
          </div>
          <div class="mb-3">
            <label for="Ciudad" class="form-label">Ciudad</label>
            <input type="text" class="form-control" id="Ciudad" aria-describedby="Ciudad"
              placeholder="ingrese su Ciudad" v-model="Ciudad">
          </div>

          <select class="form-select" aria-label="Default select example" v-model="Carrera">
            <option selected disabled>carrera</option>
            <option value="ingeneria en alimento">ingeneria en alimento</option>
            <option value="ingeneria en sistema">ingeneria en sistema</option>
            <option value="medicina">medicina</option>
            <option value="derecho">derecho</option>
          </select>
          <div class="mb-3 mt-3">
            <button type="submit" class="btn btn-primary text-black" @click="Guardar"
              v-if="($route.params.Id == 0)">Guardar</button>
          </div>
          <div class="mb-3 mt-3">
            <button type="submit" class="btn btn-primary text-black" @click="actualizar"
              v-if="($route.params.Id != 0)">actualizar</button>
          </div>
        </form>
      </div>
    </div>

  </div>

</template>
<script>
import axios from "axios"
export default {
  name: 'AgregarDatos',
  mounted() {
    // alert(this.$route.params.Id)
    if (this.$route.params.Id != 0) {
      axios.get('http://localhost/matricula_API/estudiante/' + this.$route.params.Id)
        .then((response) => {
          if (response['data'].length > 0) {
            this.Nombre = response['data'][0]['Nombre']
            this.Apellido = response['data'][0]['Apellido']
            this.Telefono = response['data'][0]['Telefono']
            this.Ciudad = response['data'][0]['Ciudad']
            this.Carrera = response['data'][0]['Carrera']
          }

        })
        .catch((error) => {
          console.log(error)
        })
    }
  },
  data() {
    return {
      Nombre: "",
      Apellido: "",
      Telefono: "",
      Ciudad: "",
      Carrera: ""
    }
  },
  methods: {
    Guardar(event) {
      event.preventDefault();

      if (this.Nombre !== "" && this.Apellido !== "" && this.Telefono !== "" && this.Ciudad !== "" && this.Carrera !== "") {

        if (this.Telefono > 0) {

          let datos = new FormData()
          datos.append("Nombre", this.Nombre)
          datos.append("Apellido", this.Apellido)
          datos.append("Telefono", this.Telefono)
          datos.append("Ciudad", this.Ciudad)
          datos.append("Carrera", this.Carrera)

          axios.post("http://localhost/matricula_API/estudiante", datos)
            .then((response) => {
              console.log(response)
              alert("estudiante ingresado correctamente")
              /* this.Nombre = ""
              this.Apellido = ""
              this.Telefono = ""
              this.Ciudad = ""
              this.Carrera = "" */
              this.$router.push('/home')
            })

            .catch((error) => {
              console.log(error)
              alert("el estudiante no fue ingresado")
            })
        }
        else {

          alert("no se aceptar valores en 0 o menores que 0 en edad")
        }
      }
      else {
        alert("rellene todos los campos")
      }
    },
    actualizar(event) {
      event.preventDefault();

      axios.put('http://localhost/matricula_API/estudiante/' + this.$route.params.Id,
        {
          "Nombre": this.Nombre,
          "Apellido": this.Apellido,
          "Telefono": this.Telefono,
          "Ciudad": this.Ciudad,
          "Carrera": this.Carrera,

        })
        .then((response) => {
          alert('estudiante actualizado correctamente')
          this.$router.push('/home')
        }).catch((error) => {
          console.log(error)
        })

    }

  },
  
}

</script>
<style>
label{
  float: left;
}
.tt{
width: 50%;

}
.card-body{
  background-color: darkgray;
}
</style>