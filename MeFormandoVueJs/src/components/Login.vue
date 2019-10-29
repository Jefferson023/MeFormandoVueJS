<template>
    <div class="container" style="width :500px; margin-top: 10%;">
    <div class="card" >  
      <div id = "login">
        <h1>Login</h1>
      </div>
    
      <!--Card content-->
      <div class="card-body px-lg-5 pt-0" style="margin-top: 20px; border-radius: 15px 15px 15px 15px;">

        <!-- Form -->
        <div class="text-center" style="color: #757575;">

          <div class="md-form" >
            <label for="email">E-mail</label>
            <input id="email" v-model="email" class="form-control" required="required">
            
          </div>

          <!-- Password -->
          <div class="md-form"> 
            <label for="password">Senha</label>
            <input type="password" id="password" v-model="password" class="form-control" required="required">
          
          </div>

          <div class="d-flex justify-content-around">
            <div>
              <!-- Remember me -->
              <div class="form-check">
                <input type="checkbox" class="form-check-input" id="materialLoginFormRemember">
                <label class="form-check-label" for="materialLoginFormRemember">Lembrar de mim</label>
              </div>
            </div>
            <div>
              <!-- Forgot password -->
              <a href="">Esqueceu a senha?</a>
            </div>
          </div>
          <!-- Sign in button -->
          <button class="btn btn-block my-4 z-depth-0" @click="logar()" >Entrar</button>

          <!-- Register -->
          <p>Ainda não tem conta?
            <a href="cadastro.html">Cadastre-se</a>
          </p>


        </div>
        <!-- Form -->

      </div>

    </div>
    <!-- Material form login -->
  </div>
</template>  

<style scoped>
    button{
        background-image:linear-gradient(to bottom, rgb(54, 0, 155), rgb(103, 43, 182));
            color:white;
        
        }
    button:before{
            
    }
    button:active{
        background-color:white;
        border: solid 2px rgba(54, 0, 155,1);
        color: rgba(54, 0, 155,1);
              
        box-shadow: 0px 0px 0px 0px;

        }
        button:focus{
              
        }
    #login{
        width:100%px;
        height: 80px;
        text-align: center;
        padding-top: 15px;
        border-radius: 5px 5px 0px 0px;
        font-family: Verdana,sans-serif;
    }
    
</style>

<script>
    import axios from 'axios';
    import qs from 'qs';
    const url = process.env.API;
    export default {
        name: 'login',
        data() {
            return {password: "", email: ""};
        },
        methods: {
            logar(){
                const data = qs.stringify({email: this.email, senha: this.password})
                const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8'}
                axios.post(process.env.API+"/usuario/logar", data, header)
                .then((response) =>{
                    console.log(response.headers);
                }).catch(()=>{
                    console.log("erro");
                })
            }
        }
    };

</script>