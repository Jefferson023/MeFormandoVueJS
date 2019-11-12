<template>
  <AppHeaderDropdown right no-caret>
    <template slot="header">
      <img
        src="img/avatars/6.jpg"
        class="img-avatar"
        alt="admin@bootstrapmaster.com" />
    </template>\
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
export default {
  name: 'DefaultHeaderDropdownAccnt',
  components: {
    AppHeaderDropdown
  },
  data: () => {
    return { itemsCount: 42 }
  },
  methods: {
    sair(){

    }
  }

}
</script>
