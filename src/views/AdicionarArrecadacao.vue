<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Arrecadação</strong></h2>
          </div>
          <b-form>
            <b-form-group
              label="Titulo"
              label-for="Titulo"
              :label-cols="3"
              >
              <b-form-input id="Titulo" v-model= "Titulo" type="text" autocomplete="titulo"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="Custo"
              label-for="Custo"
              :label-cols="3"
              >
              <b-form-input id="Custo" v-model= "Custo" type="number" prepend-icon="attach_money" autocomplete="custo"></b-form-input>
            </b-form-group>

            <b-form-group
              
              label="Ganho"
              label-for="ganho"
              :label-cols="3"
              >
              <b-form-input id="Ganho" v-model= "Ganho" type="number" prepend-icon="attach_money" autocomplete="ganho"></b-form-input>
            </b-form-group>
           
              
            <b-form-group
              label="Data Inicial" 
              label-for="DateInicial"
              :label-cols="3"
              >
              <b-form-input id="dateInicial" v-model= "dateInicial" type="date" ></b-form-input>
            </b-form-group>

            <b-form-group
              label="Data Final" 
              label-for="DateFinal"
              :label-cols="3"
              >
              <b-form-input id="dateFinal" v-model= "dateFinal" type="date" ></b-form-input>
            </b-form-group>
            
          
            <div slot="footer">
              <b-button size="xm" variant="primary" @click="criarArrecadacao()"> Criar</b-button>
              <b-button size="xm" variant="danger" to="/Arrecadacoes"> Cancelar</b-button>
            </div>
          </b-form>
      
        </b-card>
       
      </b-col>
 
    </b-row>

  </div>
</template>

<script>
import axios from 'axios';
import qs from 'qs';
export default {
  name: 'adicionarArrecadacao',
  data () {
    return {token:"",Titulo: "", Custo: "", Ganho: "", DateInicial: "", DateFinal: ""}
  },
   methods: {
    makeToast(title = null, text = null, variant = null) {
      this.$bvToast.toast(text, {
        title: title,
        variant: variant,
        toaster: "b-toaster-top-center",
        solid: true,
        autoHideDelay: 8000,
        appendToast: true
      });
    },
    criarArrecadacao(){
    if (this.Titulo != "" && this.Custo != "" && this.Ganho != "" && this.DateInicial  != null && this.DateFinal  != null ){
        const data = qs.stringify({token: localStorage.getItem('user_token') ,
        Titulo: this.Titulo, 
        Custo: this.Custo , 
        Ganho: this.Ganho , 
        DateInicial: this.DateInicial,
        DateFinal: this.DateFinal})
        axios.post(process.env.VUE_APP_API+"/arrecadacao/criar", data, {headers:{"content-type": "application/x-www-form-urlencoded;charset=utf-8",
          'token': localStorage.getItem("user_token")}}).then((response) =>{
             
            if (response.status == 201){
                this.$router.push('/arrecadacoes') 
            }else{
                this.makeToast("Erro", response.headers.erro, "danger")
            }
        }).catch(()=>{
             this.makeToast("Aviso", "Erro ao conectar com a API", "warning")
        })
    }else{
        this.makeToast("Erro", "Preencha todos os campos", "danger")
    }
    }
  }
}

</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
