<template>
  <section class="src-components-formulario">
    <div class="jumbotron mt-3">
      <vue-form :state="formState" @submit.prevent="enviarMockAPI()">
        
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text"
            id="nombre"
            class="form-control"
            autocomplete="off"
            name="nombre"
            v-model.trim="formData.nombre"
            required
            :minlength="nombreChrMin"
            :maxlength="nombreChrMax"
          >
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger my-1">Campo nombre requerido</div>
            <div slot="minlength" class="alert alert-danger my-1">Se deben ingresar como mínimo {{nombreChrMin}} caracteres</div>
            <div slot="maxlength" class="alert alert-danger my-1">Se deben ingresar como mínimo {{nombreChrMax}} caracteres</div>
          </field-messages>
        </validate>
        <br>

        <validate tag="div">
          <label for="edad">Edad</label>
          <input 
            type="number"
            id="edad"
            class="form-control"
            autocomplete="off"
            name="edad"
            v-model.number="formData.edad"
            required
            :min="edadMin"
            :max="edadMax"
          >
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger my-1">Campo edad requerido</div>
            <div slot="min" class="alert alert-danger my-1">La edad minima es de {{edadMin}} años</div>
            <div slot="max" class="alert alert-danger my-1">La edad máxima es de {{edadMax}} años</div>
          </field-messages>

        </validate>        
        <br>

        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email"
            id="email"
            class="form-control"
            autocomplete="off"
            name="email"
            v-model="formData.email"
            required
          >
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger my-1">Campo email requerido</div>
            <div slot="email" class="alert alert-danger my-1">Email no válido</div>
          </field-messages>

        </validate>
        <br>
      
        <button class="btn btn-success my-4" :disabled="formState.$invalid" type="submit">Enviar</button>
      </vue-form>
    </div>
  </section>
</template>

<script lang="js">
  export const urlUsuarios =  'https://5eac57f94bf71e00166a07e9.mockapi.io/usuarios/'
  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData : this.getInitialData(),
        edadMin: 18,
        edadMax: 120,
        nombreChrMin: 5,
        nombreChrMax: 15
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: '',
          edad: '',
          email: ''
        }
      },
      enviarMockAPI() {
        console.log(this.formData)
        /* ------------------------ */
        /* ENVIO DE DATOS CON AXIOS */
        /* ------------------------ */
        this.axios.post(urlUsuarios, this.formData, {
          'content-type' : 'application/json'
        })
        .then( res => {
          console.log(res.data)
          this.formData = this.getInitialData()
          this.formState._reset()
          this.enviando = false
        })
        .catch(error => {
          console.log('ERROR POST', error)
        })

      }
    },

    computed: {

    }
}


</script>

<style scoped lang="css">
.src-components-formulario {
}
</style>
