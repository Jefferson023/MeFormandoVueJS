<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
            <b-card no-body class="p-4">
              <b-card-body>
                <b-form>
                  <h1>Login</h1>
                  <p class="text-muted">Sign In to your account</p>
                  <b-input-group class="mb-3">
                    <b-input-group-prepend><b-input-group-text><i class="icon-user"></i></b-input-group-text></b-input-group-prepend>
                    <b-form-input v-model = "email" type="text" class="form-control" placeholder="Email" autocomplete="username email" />
                  </b-input-group>
                  <b-input-group class="mb-4">
                    <b-input-group-prepend><b-input-group-text><i class="icon-lock"></i></b-input-group-text></b-input-group-prepend>
                    <b-form-input v-model = "password" type="password" class="form-control" placeholder="Senha" autocomplete="current-password" />
                  </b-input-group>
                  <b-row>
                    <b-col cols="6">
                      <b-button @click="logar()" variant="primary" class="px-4">Login</b-button>
                    </b-col>
                    <b-col cols="6" class="text-right">
                      <b-button variant="link" class="px-0">Esqueceu sua senha?</b-button>
                    </b-col>
                  </b-row>
                </b-form>
              </b-card-body>
            </b-card>
            <b-card no-body class="text-white bg-primary py-5 d-md-down-none" style="width:44%">
              <b-card-body class="text-center">
                <div>
                  <h2>Ainda não possui sua conta?</h2>
                  <p>Venha fazer parte do MeFormando e participe da sua formatura.</p>
                  <b-button variant="primary" class="active mt-3" to="/pages/register">Registre-se agora!</b-button>
                </div>
              </b-card-body>
              <b-button v-if="DeuCerto">
                True
              </b-button>
            </b-card>
          </b-card-group>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import qs from 'qs';
export default {
  name: 'Login',
  data() {
    return {password: "", email: ""};
  },
  props:{
    DeuCerto:{
      type:Boolean,
      default: false
    }
  },
  methods: {
    logar(){
      const data = qs.stringify({email: this.email, senha: this.password})
      const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8'}
      axios.post(process.env.VUE_APP_API+"/usuario/logar", data, header).then((response) =>{
        if (response.status == 201){
          localStorage.setItem("user_token", response.headers.token)
          this.$router.push('/')  
        }else{
          alert("Algo errado1!!!")
          //usuário ou senha inválido
        }
      }).catch(()=>{
        console.log("erro");
        alert("Algo errado!!!")
        
      })
    }
  }
}  
</script>