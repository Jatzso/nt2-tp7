<template>

<div>
 <table class="table" v-if="this.usuarios.length">
  <thead>
    <tr>
      <th scope="col">Nombre</th>
      <th scope="col">Edad</th>
      <th scope="col">Mail</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(usuario,index) in usuarios" :key="index">
      <td>{{ usuario.nombre }}</td>
      <td>{{ usuario.edad }}</td>
      <td>{{ usuario.mail }}</td>
    </tr>
  </tbody>
</table>
<h3 class="alert alert-warning mt-3" v-else>No hay usuarios disponibles</h3>
</div>
</template>

<script>

  export default  {
    name: 'src-components-tabla',
    props: [],
    mounted () {
      this.getUsuarios()
    },
    data () {
      return {
        usuarios: [],
        url: 'https://628e5e53a339dfef87ad1064.mockapi.io/Usuarios',
      }
    },
    methods: {
      //Método GET con try/catch
     /*  async getUsuarios(){
        try {
          let {data:usuarios} = await this.axios(this.url)
          this.usuarios = usuarios
        } catch (error) {
          console.log(error.message)
        }
      }, */
      getUsuarios(){
         this.axios(this.url)
          .then(response => {
            let { data:respuesta } = response 
            this.usuarios = respuesta
          })
          .catch( error => console.error('Error en Axios:', error)) 
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-tabla {

  }
</style>
