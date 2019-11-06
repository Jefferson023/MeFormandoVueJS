<template>
    
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <h2><strong>Turma</strong></h2>
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
              label="Instituição"
              label-for="Instituicao"
              :label-cols="3"
              >
            <b-form-input id="Instituicao" v-model= "Instituicao" type="text"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Ano de Formação"
              label-for="AnoFormacao"
              :label-cols="3"
              >
            <b-form-input id="AnoFormacao" v-model= "AnoFormacao" type="number"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Semestre de Formação"
              label-for="SemestreFormacao"
              :label-cols="3"
              >
            <b-form-input id="SemestreFormacao" v-model= "SemestreFormacao" type="number"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Curso"
              label-for="Curso"
              :label-cols="3"
              >
            <b-form-input id="Curso" v-model= "Curso" type="text"></b-form-input>
            </b-form-group>
            
          
            <div slot="footer">
              <b-button  size="xm" variant="primary" @click="criarTurma()"> Criar</b-button>
              <b-button size="xm" variant="danger" to="/Turma"> Cancelar</b-button>
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
  name: 'criar',
  data () {
    return {token:"",Titulo: "", Instituicao: "", AnoFormacao: "", SemestreFormacao: "", Curso: ""}
  },
  methods:{
    
    criarTurma(){
      if (this.Titulo != "" && this.Instituicao != "" && this.AnoFormacao != "" 
      && this.SemestreFormacao != "" && this.Curso != ""){
           const data = qs.stringify({token: localStorage.getItem('user_token') ,Titulo: this.Titulo, Instituicao: this.Instituicao, AnoFormacao: this.AnoFormacao
          , SemestreFormacao: this.SemestreFormacao, Curso: this.Curso  })
          const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8',}
    
          axios.post(process.env.VUE_APP_API+"/turma/criar", data, header).then((response) =>{
            if (response.status == 201){
              alert("Turma Criada")
            }else if(response.status == 202){
              
              this.$router.push('/pages/404')
            }
          }).catch(()=>{
              this.$router.push('/pages/500')
          })
      }else{
        this.$router.push('/pages/500')
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
