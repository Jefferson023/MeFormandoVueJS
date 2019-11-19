<template>
  <div ass="animated fadeIn">
    <b-row>
      <b-col lg="12">
        <arrecadacao :table-data="items" :fields="fields" caption="Arrecadacao"></arrecadacao>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { shuffleArray } from "@/shared/utils";
import arrecadacao from "./Arrecadacao.vue";
import axios from "axios";
import qs from "qs";
export default {
  name: "arrecadacoes",
  components: { arrecadacao },
  data: () => {
    return {
      items: [],
      fields: [
        { key: "titulo" },
        { key: "custo" },
        { key: "ganho" },
        { key: "dateInicial" },
        { key: "dateFinal" },
        { key: "id" }
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
      .get(process.env.VUE_APP_API + "/turma/arrecadacoes", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          
          response.data.forEach(element => {
            this.items.push({
              titulo: element[0],
              custo: element[1],
              ganho: element[2],
              dateInicial: element[3],
              dateFinal: element[4],
              id: element[5]
            });
            
          });
        } else {
        }
      })
      .catch(() => {});
  }
};
</script>