<template>
  <div class="palindromo">
    <h1>Palindromo</h1>
  <b-card class="mt-3" header="Verificacao de Palavra">
    <b-form>
      <b-form-group
        id="input-group-1"
        label="Palavra:"
        label-for="input-1"
        :description="valida_palavra"
      >
        <b-form-input
          id="input-1"
          v-model="form.palavra"
          placeholder="Digite uam palavra com ao menos 3 caracteres"
          required
        ></b-form-input>
      </b-form-group>
        </b-form>
    </b-card>
  </div>
</template>
<script>
export default {
   data() {
      return {
      form: {
          palavra: ''
        },
        show: true
      }
    },
    computed:{
      valida_palavra: function(){
        
        if(this.form.palavra !== ""){
            if(this.form.palavra.length < 3){
                  return "palavra precisa ter ao menos 3 caracteres"
            }if(this.form.palavra.length >= 3){
                   var palavra = this.form.palavra.split('').reverse().join(''); 
                   if(palavra === this.form.palavra){
                        return " E um palindromo"
                   }
                  return palavra
            }
              
        }
        return ""
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
