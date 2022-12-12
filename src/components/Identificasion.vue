<template>
    <div class="container  tt">
    <div class="card mt-3">
      <div class="card-body  text-black">
        <h5 class="card-title">identificate</h5>
        <form>
          <div class="mb-3 form-group">
            <label class="form-label ">usuario</label>
            <input type="text" class="form-control" id="usuario" aria-describedby="usuario"
              placeholder="ingrese su usuario" v-model="usuario">
          </div>
          <div class="mb-3">
            <label for="constrasenia" class="form-label">constrasenia</label>
            <input type="password" class="form-control" id="contrasenia" aria-describedby="contrasenia"
              placeholder="ingrese su contraseña" v-model="contrasenia">
          </div>
          <div class="mb-3 mt-3">
            <button type="submit" class="btn btn-primary text-black" @click="ingresar">ingresar</button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>
<script>
import axios from "axios";
export default{
name:'Identificasion',
data() {
    return {
      usuario: "",
      contrasenia: ""

    }
  },
  methods: {
    ingresar(event) {

      event.preventDefault();
      axios.get('http://localhost/personal_api/usuario').then((response) => {
        response = response['data'];
        console.log(response)

        response.forEach(element => {

          if (this.usuario.toLowerCase().toString() == element.usuario.toLowerCase().toString() &&
          this.contrasenia.toLowerCase().toString() == element.contrasenia.toLowerCase().toString() )
        {

            this.$router.push('/home')
          return
        }


      });
    }).catch((error) => {
      console.log(error)
    });

  }
}


}
</script>

<style>

</style>