<template>
  <div class="animated fadeIn" v-if="tem_turma">
    <b-row>
      <b-col md="12">
        <b-card>
          <div slot="header">
            <b-row>
              <b-col md="11">
                <h2>
                  <strong>Turma: {{ titulo }}</strong>
                  <b-button
                    type="submit"
                    size="gm"
                    variant="primary"
                    style="margin-left: 75%;"
                    to="/EditarCerimonial"
                    v-if="comissao"
                  >Editar</b-button>
                </h2>
              </b-col>
            </b-row>
          </div>

          <h4><strong>Instituicao:</strong> {{ instituicao }}</h4>
          <h4><strong>Curso:</strong> {{ curso }}</h4>
          <h4><strong>Ano de Formacao:</strong> {{ periodo }}</h4>
        </b-card>
      </b-col>
    </b-row>

    <b-row>
      <b-col lg="12">
        <c-table :table-data="itensParticipantes" :fields="fieldsParticipantes" :caption="caption"></c-table>
      </b-col>
    </b-row>

    <b-row>
      <b-col lg="12">
        <c-table :table-data="itensConvidados" :fields="fieldsConvidados" :caption="captionConv"></c-table>
      </b-col>
    </b-row>
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
        to="/ConvitesDeTurma"
      >Visualizar Convites de Turma</b-button>
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
      idTurma: 0,
      titulo: "",
      instituicao: "",
      curso: "",
      qtd: "",
      periodo: "",
      caption: "",
      captionConv: "",
      itensParticipantes: [],
      itensConvidados: [],
      fieldsParticipantes: [
        { key: "username", label: "Nome", sortable: true },
        { key: "email", label: "E-mail" },
        { key: "cargo", sortable: true },
        { key: "opcoes" }
      ],
      fieldsConvidados: [
        { key: "username", label: "Nome", sortable: true },
        { key: "email", label: "E-mail" },
        { key: "status", label: "Status", sortable: true },
        { key: "opcoes" }
      ]
    };
  },
  created() {
    axios
      .get(process.env.VUE_APP_API + "/usuario/turma", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        
        if (response != null) {
          console.log(response.data);
          if (response.data[0] == true) {
            this.tem_turma = true
            this.titulo = response.data[1]
            this.instituicao = response.data[2]
            this.curso = response.data[3]
            this.periodo = response.data[4] + "." + response.data[5]
            this.qtd = response.data[6]
            this.caption = "Participantes (" + this.qtd + ")" 
            this.idTurma = response.data[7]
          } else {
            this.tem_turma = false
          }
        }
      })
      .catch(e => {
        console.log("# NAO entrei no get turma por formando ");
      });

    axios
      .get(process.env.VUE_APP_API + "/turma/formandos", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          response.data.forEach(element => {
            if (element[2] == true) {
              this.itensParticipantes.push({
                username: element[1],
                email: element[0],
                cargo: "Comissão"
              });
            } else {
              this.itensParticipantes.push({
                username: element[1],
                email: element[0],
                cargo: "Formando"
              });
            }
          });
        }
      })
      .catch(() => {});

     axios
      .get(process.env.VUE_APP_API + "/convites/convidados", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          response.data.forEach(element => {
            this.itensConvidados.push({
                username: element[0],
                email: element[1],
                status: element[2]
            })
          });
          this.captionConv = "Conviados (" + response.data.length + ")" 
        }
      })
      .catch((e) => { alert("nao pode bucar  lista de conv na api " + e) });
  }
};
</script>
