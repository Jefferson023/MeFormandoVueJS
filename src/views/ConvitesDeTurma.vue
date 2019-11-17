<template>

  <div class="animated fadeIn">
    <b-row>
      <b-col lg="12">
        <c-table :table-data="items" :fields="fields" caption="<h1>Convites</h1>"></c-table>
      </b-col>
    </b-row>
    <!--/.row-->
  </div>

</template>

<script>
import { shuffleArray } from "@/shared/utils";
import cTable from "./TableConvites.vue";
import axios from "axios";
import qs from "qs";

export default {
  name: "convites",
  components: { cTable },
  data: () => {
    return {
      items: [],
      fields: [
        { key: "turma", label: "Turma", sortable: true },
        { key: "formando", label: "Convidado por", sortable: true },
        { key: "opcoes" }
      ]
    };
  },
  created() {
    axios
      .get(process.env.VUE_APP_API + "/convites/por_convidado", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          console.log(response.data);
          response.data.forEach(element => {
            this.items.push({
              turma: element[0],
              formando: element[1],
              id: element[2],
              idConvite: element[3]
            });
          });
        } else {
        }
      })
      .catch(e => {
        alert(e);
      });
  }
};

</script>
