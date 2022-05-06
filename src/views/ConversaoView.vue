<template>
  <div class="palindromo">
    <h1>Conversor REAL/DOLAR</h1>
  <b-card class="mt-3" header="Verificacao de Palavra">
    <b-form @submit="onSubmit" >
      <b-form-group
        id="input-group-1"
        label="Palavra:"
        label-for="input-1"
      
      >
        <b-form-input
          id="input-1"
          v-model="form.valor"
          placeholder="Digite o valor em Dolar a ser convertido "
          required
        ></b-form-input>
      </b-form-group>
      <p/>
      <b-button type="submit" variant="primary" style="margin-right:10px;">Enviar</b-button>
     
        </b-form>
    </b-card>
  </div>
</template>
<script>
export default {
   data() {
      return {
      form: {
          valor: ''
        },
        show: true
      }
    },
    methods:{
          onSubmit(event) {
               event.preventDefault()
               const parametros = { valor: this.form.valor };
               this.axios.post("http://localhost:26394/mc/Converter/ConverterParaDolar", parametros).then((response) => {
                console.log(response.data)
                if(response.data.success === true){
                       this.$swal('Conversao Resolvida!',
                             "O Valor Convertido de REAL para DOLAR e de UU$:"+response.data.data.valor,
                         'success');
                }
                if(response.data.success === false){
                        this.$swal('Houve um Erro!',
                         "Houve algum erro entre a requisicao e a API de consulta",
                         'error');
                }
     })
          }
    }
}
</script>
<style scoped lang="scss">
.palindromo{
  margin: 0 auto;
  width:30%;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
