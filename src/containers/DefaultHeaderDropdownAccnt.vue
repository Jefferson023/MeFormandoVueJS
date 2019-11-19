<template>
  <AppHeaderDropdown right no-caret>
    <template slot="header">
      <!--<img src="img/avatars/6.jpg" class="img-avatar" alt="admin@bootstrapmaster.com" />-->
      <b-button variant="dark">{{nome}}</b-button>
    </template>
    <template slot="dropdown">
     
      <b-dropdown-header
        tag="div"
        class="text-center">
        <strong>Configurações</strong>
      </b-dropdown-header>
      <b-dropdown-item to="/perfil"><i class="fa fa-user"  /> Perfil</b-dropdown-item>

      <b-dropdown-divider />
      <b-dropdown-item to="/logout"><i class="fa fa-lock" /> Sair</b-dropdown-item>
    </template>
  </AppHeaderDropdown>
</template>

<script>
import { HeaderDropdown as AppHeaderDropdown } from '@coreui/vue'
import { METHODS } from 'http'
import axios from "axios"

export default {
  name: 'DefaultHeaderDropdownAccnt',
  components: {
    AppHeaderDropdown
  },
  data: () => {
    return { 
      nome: "",
      email: "",
      itemsCount: 42 
      }
  },
  created() {
    axios
      .get(process.env.VUE_APP_API + "/usuario", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response != null) {
          this.nome = response.data[0]
          this.email = response.data[1]
        }
      })
      .catch(e => {
        console.log("# Nao conectou com a API ");
      });
  },
  methods: {
    sair(){

    }
  }
}
</script>
