<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="6" sm="8">
          <b-card no-body class="mx-4">
            <b-card-body class="p-4">
              <b-form>
                <h1>Registro</h1>
                <p class="text-muted">Crie sua conta</p>
                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text><i class="icon-user"></i></b-input-group-text>
                  </b-input-group-prepend>
                  <b-form-input type="text" v-model = "nome" class="form-control" placeholder="Nome Completo" autocomplete="nome" />
                </b-input-group>

                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text>123</b-input-group-text>
                  </b-input-group-prepend>
                  <b-form-input type="text" v-model = "cpf" class="form-control" placeholder="CPF" autocomplete="cpf" />
                </b-input-group>

                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text>@</b-input-group-text>
                  </b-input-group-prepend>
                  <b-form-input type="text" v-model = "email" class="form-control" placeholder="Email" autocomplete="email" />
                </b-input-group>

                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text><i class="icon-lock"></i></b-input-group-text>
                  </b-input-group-prepend>
                  <b-form-input type="password" v-model = "senha" class="form-control" placeholder="Senha" autocomplete="new-password" />
                </b-input-group>

                <b-input-group class="mb-4">
                  <b-input-group-prepend>
                    <b-input-group-text><i class="icon-lock"></i></b-input-group-text>
                  </b-input-group-prepend>
                  <b-form-input v-model = "confirmar" type="password" class="form-control" placeholder="Confirme a senha" autocomplete="new-password" />
                </b-input-group>

                <b-button variant="success" block @click="cadastrar()" >Finalizar Cadastro</b-button>

                <b-button variant="danger" block to="/pages/login">Cancelar</b-button>
              </b-form>
            </b-card-body>
            
          </b-card>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import qs from 'qs';
export default {
  name: 'Register',
  data(){
    return {email: "", nome: "", cpf: "", senha: "", confirmar: ""}
  },
  methods:{
    cadastrar(){
      if (this.email != "" && this.nome != "" && this.cpf != "" 
      && this.senha != "" && this.senha == this.confirmar){
        const data = qs.stringify({email: this.email, senha: this.senha, nome: this.nome
        , cpf: this.cpf})
        const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8'}
        axios.post(process.env.VUE_APP_API+"/usuario/registrar", data, header).then((response) =>{
          if (response.status == 201){
            this.$router.push('/pages/login')
          }else{
            //usuário existente ou dados inválidos
          }
        }).catch(()=>{
          this.$router.push('/pages/500')
        })
      }
    }
  }

}
</script>
