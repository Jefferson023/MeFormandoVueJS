<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Cerimonial</strong></h2>
          </div>
          <b-form>
            <b-form-group
              label="Nome do Cerimonial"
              label-for="Nome"
              :label-cols="3"
              >
              <b-form-input id="Nome" v-model= "Nome" type="text" autocomplete="nome"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="Custo"
              label-for="Custo"
              :label-cols="3"
              >
              <b-form-input id="Custo" v-model= "Custo" type="number" autocomplete="custo"></b-form-input>
            </b-form-group>
           
            
            <b-form-group
            
            label="Descrição"
            label-for="basicText"
            :label-cols="3"
            >
            <b-form-input id="Descricao" v-model= "Descricao" type="text" ></b-form-input>
          </b-form-group>
          
            <div slot="footer">
              <b-button  size="xm" variant="primary" @click="alterarCerimonial()"> Alterar</b-button>
              <b-button  size="xm" variant="danger" to="/Cerimonial"> Cancelar</b-button>
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
  name: 'alterarCerimonial',
  data () {
    return {token:"",Nome: "", Custo: "", Descricao: ""}
  },
  methods: {
    alterarCerimonial(){
    if (this.Nome != "" && this.Custo != ""){
     
        const data = qs.stringify({token: localStorage.getItem('user_token') ,Nome: this.Nome, Custo: this.Custo, Descricao: this.Descricao})
        const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8',}
        axios.post(process.env.VUE_APP_API+"/cerimonial/alterar", data, header).then((response) =>{
             alert("Entrou no POST")
            if (response.status == 201){
                alert("Cerimonial alterado")
            }else{
                
                alert("Erro")
            }
        }).catch(()=>{
            alert("Erro")
        })
    }else{
        alert("Não tem todos os campos!!!")
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
