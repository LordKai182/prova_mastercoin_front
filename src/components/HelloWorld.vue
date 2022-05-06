<template>
<div>
 <div class="formulario">
  <b-card class="mt-3" header="Formulario de Cadastro">
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Nome Completo:"
        label-for="input-1"
        :description="validacao_nome_completo"
      >
        <b-form-input
          id="input-1"
          v-model="form.nome_completo"
          type="nome_completo"
          placeholder="Digite seu nome completo"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Nome de Usuario:" label-for="input-2" :description="validacao_nome">
        <b-form-input
          id="input-2"
          v-model="form.nome_usuario"
          placeholder="Digite seu Nome de Usuario"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Data de Nascimento:" label-for="input-3" :description="validacao_data">
        <b-form-datepicker 
        id="example-datepicker" 
        placeholder="Digite sua Data de Nascimento"
        v-model="form.data_nascimento" 
        class="mb-2"
        >
        </b-form-datepicker>
      </b-form-group>

       <b-form-group id="input-group-4" label="E-mail:" label-for="input-4" :description="validacao_email">
        <b-form-input
          id="input-4"
          v-model="form.email"
          placeholder="Digite seu E-mail"
          required
        ></b-form-input>
      </b-form-group>

       <b-form-group id="input-group-5" label="Senha:" label-for="input-5" :description="validacao_senha">
        <b-form-input
          type="password"
          id="input-5"
          v-model="form.senha"
          placeholder="Digite sua senha"
          required
        ></b-form-input>
      </b-form-group>

      <p/>
      <b-button type="submit" variant="primary" style="margin-right:10px;">Enviar</b-button>
      <b-button type="reset" variant="danger">Resetar</b-button>
    </b-form>
    </b-card>
    <p/>
  
  </div>
  <div  style="width:50%;margin:0 auto;">
    <b-card class="mt-3" header="Usuarios Cadastrados">
        
    <b-table striped hover :items="items" :fields="fields"></b-table>
  
    </b-card>
  </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        fields: ['nome', 'nomeUsuario', 'dataNascimento', 'email'],
        items: [
        ],
        form: {
          nome_completo: '',
          nome_usuario: '',
          data_nascimento: '',
          email: '',
          senha: ''
        },
        validacao: "validacao",
        show: true
      }
    },
    computed:{
      validacao_email: function(){
           var re = /\S+@\S+\.\S+/;
           if(!re.test(this.form.email) && this.form.email !== ""){
             console.log('dddddd')
             return "E-mail Invalido"
           }
            if(re.test(this.form.email)){
             return "E-mail Valido"
           }
           return "";
      },
      validacao_senha: function(){
         let regex = /^(?=.*[@!#$%^&*()/\\])(?=.*[0-9])(?=.*[a-zA-Z])[@!#$%^&*()/\\a-zA-Z0-9]{3,20}$/;
         if(!regex.test(this.form.senha) && this.form.senha !== ""){
           return "Senha Invalida, a senha precisa ter um numero e um caracter especial."
         }
          if(regex.test(this.form.senha)){
           return "Senha Valida."
         }
         return ""

      },
      validacao_nome_completo: function(){
        if(this.nomeSobrenome() === 0 && this.form.nome_completo !== ""){
           return " Nome completo Invalido"
        }if(this.nomeSobrenome() > 1){
           return " Nome completo Valido"
        }
         return ""
        
      },
        validacao_nome: function(){
        if(this.form.nome_usuario === 'mastercoin' || this.form.nome_usuario === 'mc'){
           return "Seu nome de usuario nao pode ser: " + this.form.nome_usuario
        }
        return ""
        
      },
      validacao_aniversario: function(){
        if(this.form.nome_usuario === 'mastercoin' || this.form.nome_usuario === 'mc'){
           return "Seu nome de usuario nao pode ser: " + this.form.nome_usuario
        }
        return ""
        
      },
      validacao_data: function(){
          if(this.form.data_nascimento !== ''){
            var dn = new Date(this.form.data_nascimento)
            console.log(dn)
            return this.idade(dn.getFullYear(),dn.getMonth(),dn.getDate())
          }
          return ""
        
      }
    },
    created() {
       this.listarUsuarios();
    },
    methods: {
    listarUsuarios(){
       const parametros = { quantidadeLista: 0 };
       this.axios.post("http://localhost:26394/mc/Usuario/ListarUsuario", parametros).then((response) => {
        console.log(response.data)
        this.items = response.data.data
     })
    },
     idade(ano_aniversario, mes_aniversario, dia_aniversario) {
       var d = new Date,
        ano_atual = d.getFullYear(),
        mes_atual = d.getMonth() + 1,
        dia_atual = d.getDate(),

           ano_aniversario2 = +ano_aniversario,
           mes_aniversario2 = +mes_aniversario,
           dia_aniversario2 = +dia_aniversario,

        quantos_anos = ano_atual - ano_aniversario;

        if (mes_atual < mes_aniversario || mes_atual == mes_aniversario && dia_atual < dia_aniversario) {
        quantos_anos--;
        }
        if(mes_atual == mes_aniversario + 1 && dia_atual == dia_aniversario + 1){
           return quantos_anos < 0 ? "Parabens voce acabou de nascer:" + 0 : " Parabens hoje voce completa " + quantos_anos + " anos de idade";
        }
       
       return quantos_anos < " Voce tem: "+0+" anos de idade" ? 0 : " Voce tem: "+ quantos_anos+" anos de idade";
     },
      nomeSobrenome(){
       var quantVet = this.form.nome_completo.split(' ');
       var count = 0
       quantVet.map( d => {
         if(d !== ''){
            count ++
         }
       })
       return count     
    
      },
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
        const parametros = { usuario: { nome: this.form.nome_completo, nomeUsuario: this.form.nome_usuario, dataNascimento: this.form.data_nascimento, senha: this.form.senha, email: this.form.email } };
        console.log(parametros)
        this.axios.post("http://localhost:26394/mc/Usuario/CadastrarUsuario", parametros).then((response) => {
        console.log(response.data.success)
        if(response.data.success === false){
          var notificacoes = response.data.notifications.map(d => {
            return d.message
          })
             this.$swal('Houve um Erro!',
                        JSON.stringify(notificacoes),
                         'error');
           
        }
         if(response.data.success === true){
              this.listarUsuarios();
               this.$swal('Sucesso! ',
                           'Voce foi cadastrado com sucesso!',
                           'success');
              
        }
     })
      
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
          this.form.nome_completo =  '',
          this.form.nome_usuario =  '',
          this.form.data_nascimento = '',
          this.form.email = '',
          this.form.senha =  ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.formulario{
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
