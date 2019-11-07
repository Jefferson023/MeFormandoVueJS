<template>
  <div class="animated fadeIn" v-if="tem_turma">
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="Participantes  da Turma"></c-table>
      </b-col>
    </b-row>
    <!--/.row-->
  </div>

  <div class="animated fadiIn" v-else>
    <b-card>
      <div slot="header">
        <h2>
          <strong>Turma</strong>
        </h2>
      </div>

      <h1>Você não faz parte de uma turma!</h1>

      <b-button
        type="submit"
        size="xm"
        variant="primary"
        style="margin-right:10px"
      >Entrar numa turma</b-button>
      <b-button type="submit" size="xm" variant="primary" to="/CriarTurma">Criar uma turma</b-button>
    </b-card>
  </div>
</template>

<script>
import { shuffleArray } from "@/shared/utils";
import cTable from "./Table.vue";
import axios from "axios";
import qs from "qs";


export default {
  name: "turma",
  data: {},
  components: { cTable },
  data: () => {
    return {
      tem_turma: false,
      items: [],
      
      fields: [
        { key: "username", label: "Nome", sortable: true },
        { key: "email", label: "E-mail" },
        { key: "cargo", sortable: true },
        { key: "opcoes" }
      ]
    };
  },

  created() {


    axios
      .get(process.env.VUE_APP_API + "/usuario/confirmadoTurma", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response.data == true) {
          this.tem_turma = true;
        } else {
          this.tem_turma = false;
        }
      })
      .catch(() => {});
      
    
    
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
              this.items.push({
                username: element[1], email: element[0], cargo: "Formando"
              })
              
            }
          });
        } else {
          
          
        }
      })
      .catch(() => {});
    
    
  }
};
</script>
