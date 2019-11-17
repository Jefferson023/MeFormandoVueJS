<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Evento</strong></h2>
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
              <b-form-input id="Custo" v-model= "Custo" type="number" autocomplete="custo"></b-form-input>
            </b-form-group>
           
              
            <b-form-group
              label="Data do Evento" 
              label-for="Date"
              :label-cols="3"
              >
              <b-form-input id="dataAtual" v-model= "dataAtual" type="date" ></b-form-input>
            </b-form-group>
            
            <b-form-group
            
            label="Descrição"
            label-for="Descricao"
            :label-cols="3"
            >
            <b-form-input id="Descricao" type="text" v-model= "Descricao" ></b-form-input>
          </b-form-group>
          
            <div slot="footer">
              <b-button size="xm" variant="primary" @click="criarEvento()"> Criar</b-button>
              <b-button size="xm" variant="danger" to="/Eventos"> Cancelar</b-button>
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
  name: 'adicionarEvento',
  data () {
    return {token:"",Titulo: "", Custo: "",Date: "", Descricao: ""}
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
    criarEvento(){
    if (this.Titulo != "" && this.Custo != "" && this.dataAtual  != null ){
        const data = qs.stringify({token: localStorage.getItem('user_token') ,Titulo: this.Titulo, Custo: this.Custo , Date: this.dataAtual, Descricao: this.Descricao})
        axios.post(process.env.VUE_APP_API+"/evento/criar", data, {headers:{"content-type": "application/x-www-form-urlencoded;charset=utf-8",
          'token': localStorage.getItem("user_token")}}).then((response) =>{
             
            if (response.status == 201){
                this.$router.push('/eventos') 
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
