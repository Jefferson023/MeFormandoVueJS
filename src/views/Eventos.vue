<template>
  <div ass="animated fadeIn">
    <b-row>
      <b-col lg="12">
        <evento :table-data="items" :fields="fields" caption="Eventos"></evento>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { shuffleArray } from "@/shared/utils";
import evento from "./Evento.vue";
import axios from "axios";
import qs from "qs";
export default {
  name: "eventos",
  components: { evento },
  data: () => {
    return {
      items: [],
      fields: [
        { key: "title" },
        { key: "description" },
        { key: "date" },
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
      .get(process.env.VUE_APP_API + "/cerimonial/eventos", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          
          response.data.forEach(element => {
            this.items.push({
              title: element[0],
              description: element[1],
              date: element[2],
              id: element[3]
            });
            
          });
        } else {
        }
      })
      .catch(() => {});
  }
};
</script>