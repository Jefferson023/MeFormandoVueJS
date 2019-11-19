<template>
  <div class="animated fadeIn">

    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="Comissao" :comissaoPagina="comissaoPagina">
          
        </c-table>
        <!--- Buttão que quero colocar como opção para menbro da (84)99999-9999
       <b-button-group size="sm" class="mx-1">
          <b-btn>New</b-btn>
          <b-btn>Edit</b-btn>
        </b-button-group>
        -->
      </b-col>
    </b-row><!--/.row-->

  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import cTable from './Table.vue'
import axios from "axios";
import qs from "qs";


export default {
  name: 'turma',
  components: {cTable},
  data: () => {
    return {
      items: [],
  
      fields: [
        {key: 'username', label: 'Nome', sortable: true},
        {key: 'email',label:'E-mail'},
        {key: 'telefone'}
      ],
      comissaoPagina:true
      
    }
  },
  created(){
    axios
      .get(process.env.VUE_APP_API + "/turma/formandos", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
         
          console.log(response.data);
          response.data.forEach(element => {
            console.log(element[1])
            console.log(element[0])
            console.log(element[2])
            if(element[2] == true){
              this.items.push({
                username: element[1], email: element[0], cargo: "Comissão"
              })
              
            }else{
            }
          });
        } else {
          
          
        }
      })
      .catch(() => {});
  }
}
</script>
