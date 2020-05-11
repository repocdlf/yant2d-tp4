<template>

  <section class="src-components-usuarios">
    <div class="jumbotron mt-3">

      <div v-if="usuarios.length > 0">
        <div class="media alert alert-info mt-4" v-for="(usuario, index) in usuarios" :key="index">
          <div class="media-body ml-3">
            <h4><u>Usuario {{ index  + 1}} - ID: {{ usuario.id }} </u></h4>
            <br>
            <p>Nombre: <b>{{ usuario.nombre }}</b></p>
            <p>Edad: <i>{{ usuario.edad }}</i></p>
            <p>Email: <i><b>{{ usuario.email }}</b></i></p>

            <button class="btn btn-danger m-3" @click="deleteUsuario(usuario.id)">BORRAR USUARIO</button>

          </div>
        </div>
      </div>
      <div v-else class="alert alert-warning mt 4">
        No hay usuarios disponibles.
      </div>

    </div>
  </section>

</template>

<script lang="js">

  export const urlUsuarios =  'https://5eac57f94bf71e00166a07e9.mockapi.io/usuarios/'

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {
      this.getUsuarios()
    },
    data () {
      return {
        usuarios : []
      }
    },
    methods: {
      /* --------------- */
      /* API REST -> GET */
      /* --------------- */
      getUsuarios() {
        this.axios(urlUsuarios)
        .then( res => {
          console.log(res.data)
          this.usuarios = res.data
        })
        .catch(error => {
          console.log('ERROR OBTENIENDO USUARIOS', error)
        })
      },

      /* ------------------ */
      /* API REST -> DELETE */
      /* ------------------ */
      deleteUsuario(id) {
        this.axios.delete(urlUsuarios+id)
        .then( res => {
          console.log(res.data)
          let offset = this.usuarios.findIndex(usuario => usuario.id == id)
          this.usuarios.splice(offset, 1)
        })
        .catch(error => {
          console.log('ERROR BORRANDO USUARIO', error)
        })
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-http {

  }

  .jumbotron {
    background-color: rgb(115, 61, 165);
    color: white;
  }

  hr {
    background-color: white;
  }



</style>