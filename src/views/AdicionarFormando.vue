<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col md="12">
        <b-card>
          <div slot="header">
            <h2>
              <strong>Formando</strong>
            </h2>
          </div>
          <b-form>

            <b-form-group label="E-mail" label-for="Email" >
              <b-form-input id="Email" v-model="Email" type="text"></b-form-input>
            </b-form-group>
            

            <div slot="footer">
              <b-button size="xm" variant="primary" @click="convidarFormando()">Convidar</b-button>
              <b-button size="xm" variant="danger" to="/Turma">Cancelar</b-button>
            </div>
          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";
import qs from "qs";
export default {
  name: "criar",
  data() {
    return {
      Email: "",

    };
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
    convidarFormando() {
      if (
        this.Email != ""
      ) {
        const data = qs.stringify({
          token: localStorage.getItem("user_token"),
          Email: this.Email,
        });

        const header = {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          'token': localStorage.getItem("user_token")
        };
        axios
          .post(process.env.VUE_APP_API + "/convites/convidar", data, {headers:{"content-type": "application/x-www-form-urlencoded;charset=utf-8",
          'token': localStorage.getItem("user_token")}})
          .then(response => {
            if (response.status == 201) {
              this.$router.push({name:'Turma'})
            }else{
              this.makeToast("Erro", response.headers.erro, "danger")
            }
          })
          .catch((e) => {
            this.makeToast("Aviso", "Desculpe, algo deu errado ao tentar conectar a API. Chama a boysinha da TI. " + e, "warning")
          });
      } else {
        this.makeToast("Erro", "E-mail obrigatorio", "danger")
      }
    }
  }
};
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
