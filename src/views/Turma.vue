<template>
  <div class="animated fadeIn" v-if="tem_turma">

    
    
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="Participantes  da Turma">
          
        </c-table>

      </b-col>

 
    </b-row><!--/.row-->

    
  </div>
  
  <div class="animated fadiIn" v-else>
    <b-card>
    <div slot="header">
        <h2><strong>Turma</strong></h2>
    </div>
    
      <h1>Você não faz parte de uma turma!</h1>
     
        <b-button type="submit" size="xm" variant="primary" style="margin-right:10px"> Entrar numa turma</b-button>
        <b-button type="submit" size="xm" variant="primary" to="/CriarTurma"> Criar uma turma</b-button>
    
    </b-card>
  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import cTable from './Table.vue'
import axios from 'axios';
import qs from 'qs';

const someData = () => shuffleArray([
  {username: 'Samppa Nori', email: 'teste@teste.com', cargo: 'Comissão' },
  {username: 'Estavan Lykos', email: 'teste@teste.com', cargo: 'Formando'},
  {username: 'Chetan Mohamed', email: 'teste@teste.com', cargo: 'Comissão'},
  {username: 'Derick Maximinus', email: 'teste@teste.com', cargo: 'Formando'},
  {username: 'Friderik Dávid', email: 'teste@teste.com', cargo: 'Formando'},

])



export default {
  name: 'turma',
  data: {
    
  },
  components: {cTable},
  data: () => {
    return {
      tem_turma: true,
      items: someData,
      itemsArray: someData(),
      fields: [
        {key: 'username', label: 'Nome', sortable: true},
        {key: 'email',label:'E-mail'},
        {key: 'cargo', sortable: true},
        {key: 'opcoes'}
      ],
      
      }
      
  },
  /*
  created()  {
        const data = qs.stringify({token: localStorage.getItem('user_token'),teste:true})
        const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8',}
        axios.get(process.env.VUE_APP_API+"/usuario/confirmadoTurma", data, header).then((response) =>{
            alert(response.data)
            if (response.data == true){
              this.tem_turma = true
            }else{
              this.tem_turma = false
            }
        }).catch(()=>{
            alert("Erro catch")
        })
    }
  */ 
}
  

 

</script>
