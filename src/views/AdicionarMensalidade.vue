<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col md="12">
        <b-card>
          <div slot="header">
            <h2>
              <strong>Adicionar Mensalidade</strong>
            </h2>
          </div>
          <b-form>
            <b-form-group label="Valor" label-for="Valor" :label-cols="3">
              <b-form-input id = "Valor" v-model="valor" type="number"></b-form-input>
            </b-form-group>

            <b-form-group label="Mes" label-for="Data" :label-cols="3">
              <b-form-input id="Data" v-model="mes" type="number"></b-form-input>
            </b-form-group>

            <div slot="footer">
              <b-button size="xm" variant="primary" @click="criarMensalidade()">Criar</b-button>
              <b-button size="xm" variant="danger" to="/pagamentos">Cancelar</b-button>
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
      valor: 0,
      mes: 1,
    };
  },
  methods: {
    criarMensalidade(){
      var d = new Date();
      var mes = this.mes.toString()
      if (mes.length == 1){
        mes = '0' + mes
      }
      var mesData = "01/"+mes+"/"+ d.getFullYear()

      const data = qs.stringify({
          token: localStorage.getItem("user_token"),
          valor: this.valor,
          mes: mesData,
        });

        axios
          .post(process.env.VUE_APP_API + "/pagamento/cadastrarMensalidade", data, {headers:{"content-type": "application/x-www-form-urlencoded;charset=utf-8",
          'token': localStorage.getItem("user_token")}})
          .then(response => {
            if (response.status == 201) {
              this.$router.push("/pagamentos")
            }else{
              console.log(response)
            }
          })
          .catch((e) => {
            alert(e);
          });
          
    }
  }
}  
</script>  